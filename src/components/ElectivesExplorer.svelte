<script>
    import electives from "../assets/csenElectives.json";

    let selectedElective = $state(null);
    let { openElectives = $bindable(true), boundElectives = $bindable([]) } =
        $props();

    function viewElective(elective) {
        selectedElective = elective;
    }
</script>

<div class="popup">
    <div class="popup-content">
        <button
            class="close-button"
            onclick={() => (openElectives = !openElectives)}>x</button
        >
        <div class="class-selector">
            {#each electives as elective}
                <div class="elective-card">
                    <h3 style="margin: 0;">{elective.name}</h3>
                    <button
                        style="padding: 0.5rem;"
                        onclick={() => viewElective(elective)}>View</button
                    >
                </div>
            {/each}
        </div>
        <div class="vertical-bar"></div>
        <div class="class-breakdown">
            {#if selectedElective}
                <div class="class-info">
                    <h3>{selectedElective.name}</h3>
                    <p>{selectedElective.quarter}</p>
                    <button
                        onclick={() =>
                            (boundElectives = [
                                ...boundElectives,
                                selectedElective,
                            ])}>Add Elective to Schedule</button
                    >
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
        width: 80%;
        height: 80%;
        overflow: scroll;
        padding-left: 1rem;
    }

    .close-button {
        position: absolute;
        right: 1rem;
        top: 1rem;
        background-color: transparent;
        border: none;
        color: white;
        font-size: 1.5rem;
    }

    .class-selector {
        width: 20%;
    }

    .elective-card {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 1rem;
    }

    .vertical-bar {
        width: 1px;
        background-color: white;
        height: 100%;
        top: 0;
        position: sticky;
    }

    .class-info {
        padding: 1rem;
    }
</style>
