<script>
    import { onMount } from "svelte";
    import GlossarySidebar from "../components/GlossarySidebar.svelte";
    import cytoscape from "cytoscape";

    let cy;
    let csen10 = $state(true);
    let csen11 = $state(false);
    let csen12 = $state(false);
    let csen20 = $state(false);
    let csen79 = $state(false);
    let csen146 = $state(false);
    let csen171 = $state(false);
    let csen177 = $state(false);
    let csen179 = $state(false);
    let csen122 = $state(false);
    let csen174 = $state(false);
    let csen175 = $state(false);
    let classes = [];

    async function fetchClasses() {
        const response = await fetch("/csenClasses.json");
        if (response.ok) {
            const glossary = await response.json();
            classes = glossary.map((term) => ({
                data: { id: term.id, name: term.name },
            }));
            updateGraph();
        }
    }

    function getVisibilityMap() {
        return {
            csen10,
            csen11,
            csen12,
            csen20,
            csen79,
            csen146,
            csen171,
            csen177,
            csen179,
            csen122,
            csen174,
            csen175,
        };
    }

    function updateGraph() {
        const visibilityMap = getVisibilityMap();
        const filteredElements = classes.filter(
            (element) => visibilityMap[element.data.id]
        );
        console.log(filteredElements);

        if (cy) {
            cy.elements().remove();
            cy.add(filteredElements);
            cy.layout({ name: "grid" }).run();
        }
    }

    $effect(() => {
        updateGraph();
    });

    onMount(() => {
        fetchClasses();
        cy = cytoscape({
            container: document.getElementById("graph"),
            elements: classes,
            style: [
                {
                    selector: "node",
                    style: {
                        "background-color": "#666",
                        label: "data(name)",
                        "text-halign": "center",
                        "text-valign": "top",
                        color: "#fff",
                        "font-size": "12px",
                        shape: "round-rectangle",
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
