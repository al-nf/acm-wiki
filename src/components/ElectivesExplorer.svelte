<script>
    import electives from "../assets/csenElectives.json";

    let selectedElective = $state(null);
    let { openElectives = $bindable(true), boundElectives = $bindable([]) } =
        $props();

    function viewElective(elective) {
        selectedElective = elective;
    }

    // This is here because comparing a $state object to an object doesn't work, so I just compared the names
    function compareElectives(elective) {
        return elective.name === selectedElective.name;
    }
</script>

<div class="popup">
    <div class="popup-content">
        <button
            class="close-button"
            onclick={() => (openElectives = !openElectives)}>x</button
        >
        <div class="class-selector">
            {#each electives as elective, index}
                <div class="elective-card">
                    <h4 style="margin: 0;">{elective.name}</h4>
                    <button
                        style="padding: 0.5em;"
                        onclick={() => viewElective(elective)}>View</button
                    >
                </div>
                {#if index !== electives.length - 1}
                    <div style="border: 1px solid white;"></div>
                {/if}
            {/each}
        </div>
        <div class="class-breakdown">
            {#if selectedElective}
                <div class="class-info">
                    <div class="class-info-header">
                        <h2>
                            {selectedElective.name} - {selectedElective.title}
                        </h2>
                        {#if selectedElective.schedule.fall}
                            <span>Fall</span>
                        {/if}
                        {#if selectedElective.schedule.winter}
                            <span>Winter</span>
                        {/if}
                        {#if selectedElective.schedule.spring}
                            <span>Spring</span>
                        {/if}
                        <span class={selectedElective.lab ? "lab" : "lab-no"}
                            >{#if !selectedElective.lab}
                                No
                            {/if} Lab</span
                        >
                    </div>
                    <p>{selectedElective.description}</p>
                    {#if selectedElective.schedule.fall}
                        <p>
                            <strong>Fall Professors: </strong>
                            {#each selectedElective.schedule.fall as prof, index}
                                {prof}{#if index < selectedElective.schedule.fall.length - 1},&nbsp;{/if}
                            {/each}
                        </p>
                    {/if}
                    {#if selectedElective.schedule.winter}
                        <p>
                            <strong>Winter Professors: </strong>
                            {#each selectedElective.schedule.winter as prof, index}
                                {prof}{#if index < selectedElective.schedule.winter.length - 1},&nbsp;{/if}
                            {/each}
                        </p>
                    {/if}
                    {#if selectedElective.schedule.spring}
                        <p>
                            <strong>Spring Professors: </strong>
                            {#each selectedElective.schedule.spring as prof, index}
                                {prof}{#if index < selectedElective.schedule.spring.length - 1},&nbsp;{/if}
                            {/each}
                        </p>
                    {/if}
                    {#if boundElectives.find(compareElectives)}
                        <button disabled>Elective is in your schedule!</button>
                    {:else}
                        <button
                            onclick={() =>
                                (boundElectives = [
                                    ...boundElectives,
                                    selectedElective,
                                ])}>Add Elective to Schedule</button
                        >
                    {/if}
                </div>
            {/if}
        </div>
    </div>
</div>

<style>
    .popup {
        position: fixed;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: rgba(0, 0, 0, 0.5);
        z-index: 1001;
    }

    .popup-content {
        display: flex;
        background-color: #08347a;
        border-radius: 5px;
        border: 2px solid white;
        width: 80%;
        height: 80%;
        position: relative;
    }

    .close-button {
        position: absolute;
        right: 0.2em;
        top: 0.2em;
        background-color: transparent;
        border: none;
        color: white;
        font-size: 1.5em;
    }

    .class-selector {
        overflow-y: auto;
        padding: 0 1em;
        min-width: 20%;
    }

    .class-selector::-webkit-scrollbar {
        width: 12px;
    }

    .class-selector::-webkit-scrollbar-track {
        background: #f1f1f1;
    }

    .class-selector::-webkit-scrollbar-thumb {
        background: #888;
        border-radius: 6px;
    }

    .class-selector::-webkit-scrollbar-thumb:hover {
        background: #555;
    }

    .elective-card {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-top: 0.5em;
        margin-bottom: 0.5em;
    }

    .elective-card h4 {
        color: white;
    }

    .class-breakdown {
        padding: 1em;
    }

    .class-info-header {
        display: flex;
        align-items: center;
        flex-wrap: wrap;
    }

    .class-info-header span {
        margin-left: 1em;
        padding: 0.5em;
        background-color: #13171f;
        color: white;
        border-radius: 5px;
    }

    .class-info-header span.lab {
        background-color: green;
    }

    .class-info-header span.lab-no {
        background-color: red;
    }

    .class-info-header h2 {
        margin: 0;
    }
</style>
