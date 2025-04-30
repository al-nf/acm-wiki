<script>
    import { onMount } from "svelte";
    import GlossarySidebar from "../components/GlossarySidebar.svelte";
    import ElectivesExplorer from "../components/ElectivesExplorer.svelte";
    import InfoPopup from "../components/InfoPopup.svelte";
    import csenClasses from "../assets/csenClasses.json";
    import csenElectives from "../assets/csenElectives.json";
    import infoIcon from "../assets/info_icon.png";
    import cytoscape from "cytoscape";

    let cy;
    let selectedNode = $state(null);
    let boundClasses = $state([]); // List of selected classes (called boundClasses because it's actually in the sidebar)
    let classes = [];
    let firstUpdate = true;

    let openElectives = $state(false);
    let boundElectives = $state([]); // Same thing as above, but bound to the electives explorer

    let openInfo = $state(false);

    // Gets the info for classes, electives, and their corresponding prereqs to be used as edges
    function fetchClasses() {
        classes = csenClasses.map((cls) => ({
            data: {
                id: cls.id,
                name: cls.name,
                title: cls.title,
                description: cls.description,
                lab: cls.lab,
                schedule: cls.schedule,
                year: cls.year,
                quarter: cls.quarter,
            },
        }));

        const electiveNodes = csenElectives.map((elective) => ({
            data: {
                id: elective.id,
                name: elective.name,
                title: elective.title,
                description: elective.description,
                lab: elective.lab,
                schedule: elective.schedule,
                year: elective.year,
                quarter: elective.quarter,
            },
        }));

        const prereqs = csenClasses.flatMap((cls) =>
            cls.preq.map((prereq) => ({
                data: {
                    id: prereq + cls.id,
                    source: prereq,
                    target: cls.id,
                },
            }))
        );

        const electivePrereqs = csenElectives.flatMap((elective) =>
            elective.preq.map((prereq) => ({
                data: {
                    id: prereq + elective.id,
                    source: prereq,
                    target: elective.id,
                },
            }))
        );

        classes = [
            ...classes,
            ...prereqs,
            ...electiveNodes,
            ...electivePrereqs,
        ];
        updateGraph();
    }

    // If a class or elective is updated, create a map of what elements should be visible
    function getVisibilityMap() {
        const visibilityMap = {};

        boundClasses.forEach((cls) => {
            visibilityMap[cls.id] = true;
        });

        boundElectives.forEach((elective) => {
            visibilityMap[elective.id] = true;
        });

        return visibilityMap;
    }

    // Ok, there's a lot here
    function updateGraph() {
        // Gets the visible elements and applies that as a filter to all classes and edges
        const visibilityMap = getVisibilityMap();
        const filteredElements = classes.filter(
            (element) =>
                visibilityMap[element.data.id] ||
                (element.data.source &&
                    visibilityMap[element.data.source] &&
                    visibilityMap[element.data.target])
        );

        if (cy) {
            const existingElements = cy.elements();
            const newElements = filteredElements.filter(
                (element) =>
                    !existingElements.some((el) => el.id() === element.data.id)
            );

            // only re-render new elements, keep the old ones where they are
            cy.add(newElements);
            cy.remove(
                existingElements.filter(
                    (el) =>
                        !filteredElements.some(
                            (element) => element.data.id === el.id()
                        )
                )
            );

            // ngl this is a lot of Copilot code, but it basically positions the elements in a grid
            // according to their year and quarter and uses some math to make them spaced out
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

            let trueElements = firstUpdate ? filteredElements : newElements;
            firstUpdate = false;
            filteredElements.forEach((element) => {
                if (element.data.year && element.data.quarter) {
                    const key = `${element.data.year}-${element.data.quarter}`;
                    const col = element.data.year - 1;
                    const row = element.data.quarter - 1;
                    const positionIndex = yearQuarterPositions[key]++;
                    const numElementsInCell = yearQuarterCounts[key];
                    const cellWidth =
                        colWidth / Math.ceil(Math.sqrt(numElementsInCell));
                    const cellHeight =
                        rowHeight / Math.ceil(Math.sqrt(numElementsInCell));
                    const x =
                        col * colWidth +
                        (positionIndex %
                            Math.ceil(Math.sqrt(numElementsInCell))) *
                            cellWidth +
                        cellWidth / 2 +
                        50;
                    const y =
                        row * rowHeight +
                        Math.floor(
                            positionIndex /
                                Math.ceil(Math.sqrt(numElementsInCell))
                        ) *
                            cellHeight +
                        cellHeight / 2 +
                        30;
                    if (
                        trueElements.some(
                            (el) => el.data.id === element.data.id
                        )
                    ) {
                        positions[element.data.id] = { x, y };
                    }
                }
            });

            // Adds labels for the years and quarters, which are just nodes hidden offscreen
            const labelNodes = [];
            for (let year = 1; year <= 4; year++) {
                labelNodes.push({
                    data: { id: `year-${year}`, name: `Year ${year}` },
                    position: {
                        x: (year - 1) * colWidth + colWidth / 2 + 50,
                        y: 10,
                    },
                });
            }
            for (let quarter = 1; quarter <= 3; quarter++) {
                labelNodes.push({
                    data: {
                        id: `quarter-${quarter}`,
                        name:
                            quarter === 1
                                ? "Fall"
                                : quarter === 2
                                  ? "Winter"
                                  : "Spring",
                    },
                    position: {
                        x: 10,
                        y: (quarter - 1) * rowHeight + rowHeight / 2 + 30,
                    },
                });
            }

            cy.add(labelNodes);

            cy.layout({
                name: "preset",
                positions: positions,
            }).run();
        }
    }

    // When the page mounts, make the graph and define it's styling
    // ts-ignore is used because it errors even though it's valid cytoscape syntax
    onMount(() => {
        document.title = "CSEN Glossary - SCU ACM Wiki";
        fetchClasses();
        cy = cytoscape({
            container: document.getElementById("graph"),
            elements: classes,
            zoomingEnabled: false,
            panningEnabled: false,
            style: [
                {
                    selector: "node",
                    style: {
                        width: "label",
                        height: "label",
                        content: "data(name)",
                        shape: "round-rectangle",
                        // @ts-ignore
                        padding: "0.5em",
                        "font-size": "1em",
                        "text-valign": "center",
                        "text-halign": "center",
                        "border-width": 1,
                        "border-color": "#08347a",
                    },
                },
                {
                    selector: "node[id *= 'csen']",
                    style: {
                        backgroundColor: "#d9ead3",
                        color: "#0f5132",
                    },
                },
                {
                    selector: "node[id *= 'ecen']",
                    style: {
                        backgroundColor: "#fff2cc",
                        color: "#654500",
                    },
                },
                {
                    selector: "node[id *= 'math'], node[id *= 'amth']",
                    style: {
                        backgroundColor: "#EE8489",
                        color: "#8B0000",
                    },
                },
                {
                    selector: "node[id *= 'phys'], node[id *= 'chem']",
                    style: {
                        backgroundColor: "#c9daf8",
                        color: "#005ea2",
                    },
                },
                {
                    selector: "edge",
                    style: {
                        width: 3,
                        "target-arrow-color": "#ccc",
                        "target-arrow-shape": "triangle",
                        "curve-style": "bezier",
                    },
                },
                {
                    selector: "edge[source *= 'csen']",
                    style: {
                        "line-color": "#0f5132",
                    },
                },
                {
                    selector: "edge[source *= 'ecen']",
                    style: {
                        "line-color": "#654500",
                    },
                },
                {
                    selector: "edge[source *= 'math'], edge[source *= 'amth']",
                    style: {
                        "line-color": "#8B0000",
                    },
                },
                {
                    selector: "edge[source *= 'phys'], edge[source *= 'chem']",
                    style: {
                        "line-color": "#005ea2",
                    },
                },
                {
                    selector: "node[id *= 'year']",
                    style: {
                        width: 1,
                        height: 1,
                        // @ts-ignore
                        padding: "0",
                        label: "data(name)",
                        "text-outline-width": 1,
                        "text-outline-color": "#666",
                        "text-halign": "center",
                        "text-valign": "bottom",
                        color: "#fff",
                        "font-size": "1.2em",
                        shape: "diamond",
                    },
                },
                {
                    selector: "node[id *= 'quarter']",
                    style: {
                        width: 1,
                        height: 1,
                        // @ts-ignore
                        padding: "0",
                        label: "data(name)",
                        "text-outline-width": 1,
                        "text-outline-color": "#666",
                        "text-halign": "right",
                        "text-valign": "center",
                        color: "#fff",
                        "font-size": "1.2em",
                        shape: "diamond",
                    },
                },
            ],
        });

        cy.on("tap", "node", (event) => {
            const node = event.target;
            const id = node.id();
            selectedNode = classes.find((cls) => cls.data.id === id);
        });
    });

    // This runs every time boundClasses or boundElectives is updated (thanks svelte)
    $effect(() => {
        updateGraph();
    });
</script>

<div class="glossary">
    <!-- if the width is below 1000px it kinda just breaks, maybe something for later -->
    {#if screen.width < 1000}
        <h1>
            The glossary needs to be viewed on a wider screen to work properly
        </h1>
    {:else}
        <GlossarySidebar
            bind:boundClasses
            bind:openElectives
            bind:boundElectives
        />
        <div class="graph-container">
            <div class="graph-header">
                <h1>CSEN Glossary | 2025-2026</h1>
                <button onclick={() => (openInfo = !openInfo)}>
                    <img src={infoIcon} alt="information button" />
                </button>
            </div>
            <div id="graph" class="graph"></div>
            {#if selectedNode}
                <div class="node-info">
                    <div class="node-info-header">
                        <h2>
                            {selectedNode.data.name} - {selectedNode.data.title}
                        </h2>
                        {#if selectedNode.data.schedule.fall}
                            <span>Fall</span>
                        {/if}
                        {#if selectedNode.data.schedule.winter}
                            <span>Winter</span>
                        {/if}
                        {#if selectedNode.data.schedule.spring}
                            <span>Spring</span>
                        {/if}
                        <span class={selectedNode.data.lab ? "lab" : "lab-no"}
                            >{#if !selectedNode.data.lab}
                                No
                            {/if} Lab</span
                        >
                    </div>
                    <p>{selectedNode.data.description}</p>
                    {#if selectedNode.data.schedule.fall}
                        <p>
                            <strong>Fall Professors: </strong>
                            {#each selectedNode.data.schedule.fall as prof, index}
                                {prof}{#if index < selectedNode.data.schedule.fall.length - 1},&nbsp;{/if}
                            {/each}
                        </p>
                    {/if}
                    {#if selectedNode.data.schedule.winter}
                        <p>
                            <strong>Winter Professors: </strong>
                            {#each selectedNode.data.schedule.winter as prof, index}
                                {prof}{#if index < selectedNode.data.schedule.winter.length - 1},&nbsp;{/if}
                            {/each}
                        </p>
                    {/if}
                    {#if selectedNode.data.schedule.spring}
                        <p>
                            <strong>Spring Professors: </strong>
                            {#each selectedNode.data.schedule.spring as prof, index}
                                {prof}{#if index < selectedNode.data.schedule.spring.length - 1},&nbsp;{/if}
                            {/each}
                        </p>
                    {/if}
                </div>
            {:else}
                <div class="node-info">
                    <h2>Select a class to view more information</h2>
                </div>
            {/if}
        </div>
        {#if openElectives}
            <ElectivesExplorer bind:openElectives bind:boundElectives />
        {/if}
        {#if openInfo}
            <InfoPopup bind:openInfo />
        {/if}
    {/if}
</div>

<style>
    .glossary {
        display: flex;
        margin-top: 1em;
    }

    .graph-container {
        width: 80%;
    }

    .graph-header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 0.5em;
    }

    .graph-header h1 {
        margin-bottom: 0;
    }

    .graph-header button {
        background-color: transparent;
        border: none;
        cursor: pointer;
    }

    .graph-header button img {
        width: 2em;
    }

    .graph {
        width: 75vw;
        height: 85vh;
        border: 1px solid #08347a;
    }

    .node-info {
        margin-top: 1em;
        color: white;
    }

    .node-info-header {
        display: flex;
        align-items: center;
        flex-wrap: wrap;
    }

    .node-info-header span {
        margin-left: 1em;
        padding: 0.5rem;
        background-color: #08347a;
        color: white;
        border-radius: 5px;
    }

    .node-info-header span.lab {
        background-color: green;
    }

    .node-info-header span.lab-no {
        background-color: red;
    }
</style>
