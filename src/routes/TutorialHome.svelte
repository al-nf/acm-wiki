<script>
    import { Link } from "svelte-routing";
    import TutorialCard from "../components/TutorialCard.svelte";

    let tutorials = [
        {
            "name": "C",
            "link": "tutorials/c",
            "imgSrc": "https://upload.wikimedia.org/wikipedia/commons/1/19/C_Logo.png"
        },
        {
            "name": "Python",
            "link": "tutorials/python",
            "imgSrc": "https://upload.wikimedia.org/wikipedia/commons/thumb/c/c3/Python-logo-notext.svg/1869px-Python-logo-notext.svg.png"
        },
        {
            "name": "JavaScript",
            "link": "tutorials/javascript",
            "imgSrc": "https://upload.wikimedia.org/wikipedia/commons/thumb/6/6a/JavaScript-logo.png/640px-JavaScript-logo.png"
        }
    ];
</script>

<main>
    <h1>Tutorials</h1>
    <div>
        {#each tutorials as tut}
        <TutorialCard name={tut["name"]} link={tut["link"]} imgSrc={tut["imgSrc"]}/>
        {/each}
    </div>
</main>

<style>
    div {
        display: flex;
        flex-wrap: wrap;
        gap: 1rem;
    }
</style>