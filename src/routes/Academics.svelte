<script>
    import { onMount } from "svelte";
    import { Link } from "svelte-routing";

    onMount(() => {
        document.title = "Academics - SCU ACM Wiki";
    });
</script>

<main>
    <h1>Academics</h1>
    <Link to="academics/csen-glossary">CSEN Glossary</Link>
</main>
