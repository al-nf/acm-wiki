<script>
    import { Link } from "svelte-routing";

    let {route, name} = $props();
</script>

<style>
    div {
        text-decoration: none;
        color: white;
        width: 100%;
        padding: 1rem;
    }
    div:is(:hover, :active){
        color:aqua;
    }
</style>

<Link to={route} class="link">
    <div>
        {name}
    </div>
</Link>

