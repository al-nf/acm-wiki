<script lang="ts">
    import { marked } from 'marked';
    import { onMount } from 'svelte';

    export let name: string;
    export let html: string = "<p>file not found</p>";

    onMount(async () => {
        const response = await fetch('/tutorials/'+name+'.md', {method: "GET"});
        if (response.ok) {
            const fileContent = await marked(await response.text());
            // console.log(fileContent);
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