<script lang="ts">
    import { marked } from "marked";
    import { onMount } from "svelte";

    let { path } = $props();
    let markdownContent = $state("<p>Loading...</p>");
    let solution = $state("<p>file not found</p>");
    let solutionToggle = $state(false);
    let showSolution = $state(false);

    const renderer = {
        heading({ tokens, depth }) {
            const text = this.parser.parseInline(tokens);
            const escapedText = text.toLowerCase().replace(/[^\w]+/g, "-");

            return `
                <h${depth} id="${escapedText}">
                    ${text}
                </h${depth}>`;
        },
        link({ tokens, href }) {
            const text = this.parser.parseInline(tokens);
            const isExternalLink = !href.startsWith("#");
            const target = isExternalLink ? 'target="_blank"' : "";
            return `<a href="${href}" target="${target}">${text}</a>`;
        },
    };

    marked.use({ renderer });

    onMount(async () => {
        const response = await fetch(path + ".md");
        const solutionFile = await fetch(path + "_solution.md");  
        console.log(response);  
        if (response.ok) {
            const responseContent = await response.text();
            if (responseContent.includes("<!doctype html>")) {
                markdownContent = "<p>file not found</p>"

                console.error("Failed to fetch markdown file.");
                return;
            }
            markdownContent = await marked.parse(responseContent);

            const solutionContent = await solutionFile.text();
            if (!solutionContent.includes('<meta charset="UTF-8" />')) {
                solution = await marked.parse(solutionContent);
                showSolution = true;
            }
        } else {
            markdownContent = "<p>file not found</p>"

            console.error("Failed to fetch markdown file.");
        }
    });

    function handleLinkClick(event: MouseEvent) {
        const target = event.target as HTMLElement;
        if (
            target.tagName === "A" &&
            target.getAttribute("href")?.startsWith("#")
        ) {
            event.preventDefault();
            const id = target.getAttribute("href")?.substring(1);
            const element = document.getElementById(id);
            if (element) {
                element.scrollIntoView({ behavior: "smooth" });
            }
        }
    }

    function handleSolutionToggle() {
        solutionToggle = !solutionToggle;
    }
</script>

<svelte:window on:click={handleLinkClick} />

<div class="container">
    {@html markdownContent}
    {#if showSolution}
        <button onclick={handleSolutionToggle}>
            {#if solutionToggle}
                Hide Solution
            {:else}
                Show Solution
            {/if}
        </button>
    {/if}
    <div class="spacer">
        {#if solutionToggle}
            {@html solution}
        {/if}
    </div>
</div>

<style>
    .container {
        margin: 2rem;
    }
    .spacer {
        margin-top: 1rem;
    }
</style>
