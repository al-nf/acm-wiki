<script>
    import {Link} from "svelte-routing";

    let {name, link, imgSrc} = $props();
</script>

<Link to={link}>
<div class="card">
    <img src={imgSrc} alt="logo">
    <h3>{name}</h3>
</div>
</Link>

<style>
    div.card {
        box-shadow: 0px 0px 5px gray;
        border-radius: 20px;
        text-align: center;
        padding: 1em;
        height: auto;
        align-content: center;
        align-items: center;
        width: 12em;
        margin-block: 1rem;
    }
    h3 {
        margin-bottom: 0;
        color: white;
        text-decoration: underline;
    }
    div.card:hover h3 {
        color: aqua;
    }
    img {
        width: 2rem;
    }

</style>