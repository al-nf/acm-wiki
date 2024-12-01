<script lang="ts">
    import { marked } from "marked";
    import { onMount } from "svelte";

    let { name } = $props();
    let tutorial = $state("<p>file not found</p>");
    let solution = $state("<p>file not found</p>");
    let solutionToggle = $state(false);

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
        const response = await fetch("/tutorials/" + name + ".md");
        const solutionFile = await fetch("/tutorials/" + name + "_solution.md");
        if (response.ok) {
            const responseContent = await response.text();
            const solutionContent = await solutionFile.text();
            if (responseContent.includes("<!doctype html>")) {
                console.error("Failed to fetch markdown file.");
                return;
            }
            tutorial = await marked.parse(responseContent);
            solution = await marked.parse(solutionContent);
        } else {
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
    {@html tutorial}
    <button onclick={handleSolutionToggle}>
        {#if solutionToggle}
            Hide Solution
        {:else}
            Show Solution
        {/if}
    </button>
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
