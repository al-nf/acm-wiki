<script>
    import { Link } from "svelte-routing";

    let {route, name} = $props();
</script>

<style>
    div {
        padding: 1rem;
        text-decoration: none;
        color: white;
    }
    div:hover{
        background-color: #08347A;
    }
</style>

<Link to={route}>
    <div>
        {name}
    </div>
</Link>

