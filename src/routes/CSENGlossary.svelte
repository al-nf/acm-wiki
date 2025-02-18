<script>
    import { onMount } from "svelte";
    import GlossarySidebar from "../components/GlossarySidebar.svelte";
    import ElectivesExplorer from "../components/ElectivesExplorer.svelte";
    import csenClasses from "../assets/csenClasses.json";
    import csenElectives from "../assets/csenElectives.json";
    import cytoscape from "cytoscape";

    let cy;
    let selectedNode = $state(null);
    let boundClasses = $state([]);
    let classes = [];

    let openElectives = $state(false);
    let boundElectives = $state([]);

    function fetchClasses() {
        classes = csenClasses.map((term) => ({
            data: {
                id: term.id,
                name: term.name,
                title: term.title,
                description: term.description,
                schedule: term.schedule,
                year: term.year,
                quarter: term.quarter,
            },
        }));
        const prereqs = csenClasses.flatMap((term) =>
            term.preq.map((prereq) => ({
                data: {
                    id: prereq + term.id,
                    source: prereq,
                    target: term.id,
                },
            }))
        );

        const electiveNodes = csenElectives.map((elective) => ({
            data: {
                id: elective.id,
                name: elective.name,
                year: elective.year,
                quarter: elective.quarter,
            },
        }));
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

    function getVisibilityMap() {
        const visibilityMap = {};

        boundClasses.forEach((course) => {
            visibilityMap[course.id] = true;
        });

        boundElectives.forEach((elective) => {
            visibilityMap[elective.id] = true;
        });

        return visibilityMap;
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
                        cellWidth / 2;
                    const y =
                        row * rowHeight +
                        Math.floor(
                            positionIndex /
                                Math.ceil(Math.sqrt(numElementsInCell))
                        ) *
                            cellHeight +
                        cellHeight / 2;
                    positions[element.data.id] = { x, y };
                }
            });

            const labelNodes = [];
            for (let year = 1; year <= 4; year++) {
                labelNodes.push({
                    data: { id: `year-${year}`, name: `Year ${year}` },
                    position: {
                        x: (year - 1) * colWidth + colWidth / 2,
                        y: -15,
                    },
                });
            }
            for (let quarter = 1; quarter <= 3; quarter++) {
                labelNodes.push({
                    data: {
                        id: `quarter-${quarter}`,
                        name: `Quarter ${quarter}`,
                    },
                    position: {
                        x: -15,
                        y: (quarter - 1) * rowHeight + rowHeight / 2,
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

    onMount(() => {
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
                        "background-color": "#fff",
                        label: "data(name)",
                        "text-outline-width": 1,
                        "text-outline-color": "#666",
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
                        "curve-style": "segments",
                    },
                },
                {
                    selector: "node[id *= 'year']",
                    style: {
                        label: "data(name)",
                        "text-outline-width": 1,
                        "text-outline-color": "#666",
                        "text-halign": "center",
                        "text-valign": "bottom",
                        color: "#fff",
                        "font-size": "20px",
                        shape: "diamond",
                    },
                },
                {
                    selector: "node[id *= 'quarter']",
                    style: {
                        label: "data(name)",
                        "text-outline-width": 1,
                        "text-outline-color": "#666",
                        "text-halign": "right",
                        "text-valign": "center",
                        color: "#fff",
                        "font-size": "20px",
                        shape: "diamond",
                    },
                },
            ],
        });

        cy.on("mouseover", "node", (event) => {
            const node = event.target;
            node.style("background-color", "#08347A");
        });

        cy.on("mouseout", "node", (event) => {
            const node = event.target;
            node.style("background-color", "#fff");
        });

        cy.on("tap", "node", (event) => {
            const node = event.target;
            const id = node.id();
            selectedNode = classes.find((element) => element.data.id === id);
        });
    });

    $effect(() => {
        updateGraph();
    });
</script>

<div class="glossary">
    <GlossarySidebar bind:boundClasses bind:openElectives bind:boundElectives />
    <div class="graph-container">
        <h1>CSEN Glossary</h1>
        <div id="graph" class="graph"></div>
        {#if selectedNode}
            <div class="node-info">
                <h2>{selectedNode.data.name} - {selectedNode.data.title}</h2>
                <p>{selectedNode.data.description}</p>
                <p>{selectedNode.data.schedule.fall[0]}</p>
            </div>
        {/if}
    </div>
    {#if openElectives}
        <ElectivesExplorer bind:openElectives bind:boundElectives />
    {/if}
</div>

<style>
    .glossary {
        display: flex;
        margin-top: 1rem;
    }

    .graph-container {
        width: 80%;
        padding: 1rem;
    }

    .graph {
        width: 75vw;
        height: 70vh;
        border: 1px solid #08347a;
    }

    .node-info {
        margin-top: 1rem;
        color: white;
    }
</style>
