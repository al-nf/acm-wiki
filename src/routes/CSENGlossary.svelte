<script>
    import { onMount } from "svelte";
    import GlossarySidebar from "../components/GlossarySidebar.svelte";
    import cytoscape from "cytoscape";

    let cy;
    let csen10 = false;
    let csen11 = false;
    let csen12 = false;
    let csen20 = false;
    let csen79 = false;
    let csen146 = false;
    let csen171 = false;
    let csen177 = false;
    let csen179 = false;
    let csen122 = false;
    let csen174 = false;
    let csen175 = false;

    $: console.log(csen10);

    onMount(() => {
        cy = cytoscape({
            container: document.getElementById("graph"),
            elements: [
                { data: { id: "a", name: "Node A" } },
                { data: { id: "b", name: "Node B" } },
                {
                    data: {
                        id: "ab",
                        source: "a",
                        target: "b",
                    },
                },
            ],
            style: [
                {
                    selector: "node",
                    style: {
                        "background-color": "#666",
                        label: "data(name)",
                        "text-valign": "center",
                        color: "#fff",
                        "font-size": "12px",
                        shape: "round-rectangle",
                        width: "label",
                        height: "label",
                        padding: "10px",
                    },
                },
            ],
        });
    });
</script>

<div class="glossary">
    <GlossarySidebar
        bind:csen10
        bind:csen11
        bind:csen12
        bind:csen20
        bind:csen79
        bind:csen146
        bind:csen171
        bind:csen177
        bind:csen179
        bind:csen122
        bind:csen174
        bind:csen175
    />
    <div class="graph-container">
        <h1>CSEN Glossary</h1>
        <div id="graph" class="graph"></div>
    </div>
</div>

<style>
    .glossary {
        display: flex;
        margin-top: 1rem;
        height: 90vh;
    }

    .graph-container {
        width: 70%;
        padding: 1rem;
    }

    .graph {
        width: 100%;
        height: 90%;
        border: 1px solid black;
    }
</style>
