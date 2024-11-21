<script lang="ts">
  import { marked } from "marked";
  import { onMount } from "svelte";

  export let name: string;
  export let html: string = "<p>file not found</p>";

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
    if (response.ok) {
      const fileContent = await response.text();
      if (fileContent.includes("<!doctype html>")) {
        console.error("Failed to fetch markdown file.");
        return;
      }
      html = await marked.parse(fileContent);
    } else {
      console.error("Failed to fetch markdown file.");
    }
  });
</script>

<div>
  <p>{name}</p>
  <div>{@html html}</div>
</div>

<style>
  div {
    margin: 1rem;
  }
</style>
