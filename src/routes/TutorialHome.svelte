<script>
    import { Link } from "svelte-routing";
    import { onMount } from "svelte";

    onMount(() => {
        document.title = "Tutorials - SCU ACM Wiki";
    });
</script>

<div>
    <h1>Tutorials</h1>
    <Link to="tutorials/c">C</Link>
    <Link to="tutorials/java">Java</Link>
    <Link to="tutorials/python">Python</Link>
    <Link to="tutorials/javascript">Javascript</Link>
</div>
