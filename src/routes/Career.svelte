<script>
    import { onMount } from "svelte";
    import { Link } from "svelte-routing";

    onMount(() => {
        document.title = "Career - SCU ACM Wiki";
    });
</script>

<main>
    <h1>Career Resources</h1>
    <Link to="career/resume-guide">Resume Guide</Link>
</main>
