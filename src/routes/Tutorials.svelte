<script lang="ts">
    import { marked } from 'marked';
    import { onMount } from 'svelte';

    export let name: string;
    export let html: string = "<p>file not found</p>";

    onMount(async () => {
        const response = await fetch('/tutorials/'+name+'.md')
        if (response.ok) {
            const fileContent = await response.text();
            if (fileContent.includes('<!doctype html>')) {
                console.error('Failed to fetch markdown file.');
                return;
            }
            html = await marked.parse(fileContent);
        } else {
            console.error('Failed to fetch markdown file.');
        }
    });

</script>

<div>
    <p>{name}</p>
    <div>{@html html}</div>
</div>