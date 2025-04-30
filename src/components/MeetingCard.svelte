<script>
    let {name, slides, event, year, quarter} = $props();
</script>

<div class="card">
    <h3>{name}</h3>
    <a href={slides} target="_blank">Link to Slides</a>
    <p>{quarter} {year}</p>
    <p>{event}</p>
</div>

<style>
    div.card {
        box-shadow: 0px 0px 5px gray;
        border-radius: 20px;
        text-align: left;
        padding: 1em;
        height: auto;
        align-content: center;
        align-items: center;
        margin-block: 1rem;
    }
</style>