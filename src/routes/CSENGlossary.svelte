<script>
    import { onMount } from "svelte";
    import GlossarySidebar from "../components/GlossarySidebar.svelte";
    import ElectivesExplorer from "../components/ElectivesExplorer.svelte";
    import cytoscape from "cytoscape";

    let cy;
    let csen10 = $state(false);
    let csen11 = $state(false);
    let csen12 = $state(false);
    let csen20 = $state(false);
    let csen19 = $state(false);
    let csen79 = $state(false);
    let csen146 = $state(false);
    let csen171 = $state(false);
    let csen177 = $state(false);
    let csen179 = $state(false);
    let csen122 = $state(false);
    let csen174 = $state(false);
    let csen175 = $state(false);
    let ecen21 = $state(false);
    let ecen50 = $state(false);
    let ecen153 = $state(false);
    let classes = [];

    let openElectives = $state(false);

    async function fetchClasses() {
        const response = await fetch("/csenClasses.json");
        if (response.ok) {
            const glossary = await response.json();
            classes = glossary.map((term) => ({
                data: {
                    id: term.id,
                    name: term.name,
                    year: term.year,
                    quarter: term.quarter,
                },
            }));
            const prereqs = glossary.flatMap((term) =>
                term.preq.map((prereq) => ({
                    data: {
                        id: prereq + term.id,
                        source: prereq,
                        target: term.id,
                    },
                }))
            );
            classes = [...classes, ...prereqs];
            updateGraph();
        }
    }

    function getVisibilityMap() {
        return {
            csen10: !csen10,
            csen11: !csen11,
            csen12: !csen12,
            csen20: !csen20,
            csen19: !csen19,
            csen79: !csen79,
            csen146: !csen146,
            csen171: !csen171,
            csen177: !csen177,
            csen179: !csen179,
            csen122: !csen122,
            csen174: !csen174,
            csen175: !csen175,
            ecen21: !ecen21,
            ecen50: !ecen50,
            ecen153: !ecen153,
        };
    }

    function updateGraph() {
        const visibilityMap = getVisibilityMap();
        const filteredElements = classes.filter(
            (element) =>
                visibilityMap[element.data.id] ||
                (element.data.source &&
                    visibilityMap[element.data.source] &&
                    visibilityMap[element.data.target])
        );

        if (cy) {
            cy.elements().remove();
            cy.add(filteredElements);

            const yearQuarterCounts = {};
            filteredElements.forEach((element) => {
                if (element.data.year && element.data.quarter) {
                    const key = `${element.data.year}-${element.data.quarter}`;
                    if (!yearQuarterCounts[key]) {
                        yearQuarterCounts[key] = 0;
                    }
                    yearQuarterCounts[key]++;
                }
            });

            const yearQuarterPositions = {};
            Object.keys(yearQuarterCounts).forEach((key) => {
                yearQuarterPositions[key] = 0;
            });

            const positions = {};
            const containerWidth = cy.width();
            const containerHeight = cy.height();
            const colWidth = containerWidth / 4;
            const rowHeight = containerHeight / 3;

            filteredElements.forEach((element) => {
                if (element.data.year && element.data.quarter) {
                    const key = `${element.data.year}-${element.data.quarter}`;
                    const col = element.data.year - 1;
                    const row = element.data.quarter - 1;
                    const positionIndex = yearQuarterPositions[key]++;
                    const x =
                        col * colWidth +
                        positionIndex * (colWidth / yearQuarterCounts[key]);
                    const y = row * rowHeight + rowHeight / 2;
                    positions[element.data.id] = { x, y };
                }
            });

            cy.layout({
                name: "preset",
                positions: positions,
            }).run();
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
                {
                    selector: "edge",
                    style: {
                        width: 3,
                        "line-color": "red",
                        "target-arrow-color": "#ccc",
                        "target-arrow-shape": "triangle",
                        "curve-style": "bezier",
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
        bind:csen19
        bind:csen79
        bind:csen146
        bind:csen171
        bind:csen177
        bind:csen179
        bind:csen122
        bind:csen174
        bind:csen175
        bind:ecen21
        bind:ecen50
        bind:ecen153
        bind:openElectives
    />
    <div class="graph-container">
        <h1>CSEN Glossary</h1>
        <div id="graph" class="graph"></div>
    </div>
    {#if openElectives}
        <ElectivesExplorer bind:openElectives />
    {/if}
</div>

<style>
    .glossary {
        display: flex;
        margin-top: 1rem;
    }

    .graph-container {
        width: 70%;
        padding: 1rem;
    }

    .graph {
        width: 100%;
        height: 70%;
        border: 1px solid black;
    }
</style>
