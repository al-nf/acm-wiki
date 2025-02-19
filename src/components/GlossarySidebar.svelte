<script>
    import csenClasses from "../assets/csenClasses.json";
    import trashIcon from "../assets/trash_can_icon.png";

    let {
        boundClasses = $bindable([]),
        openElectives = $bindable(false),
        boundElectives = $bindable([]),
    } = $props();

    let classes = $state(csenClasses);

    classes.forEach((course) => {
        course["checked"] = false;
    });

    const csenCores = classes.filter((course) => course.id.includes("csen"));
    const ecenCores = classes.filter((course) => course.id.includes("ecen"));

    $effect(() => {
        let newBoundClasses = [];
        classes.forEach((course) => {
            if (!course["checked"]) {
                newBoundClasses.push(course);
            }
        });
        boundClasses = newBoundClasses;
    });
</script>

<div class="sidebar">
    <h2>Select classes you've taken</h2>
    <div class="sidebar-elements">
        <div class="sidebar-section">
            <h3>CSEN Cores</h3>
            {#each csenCores as course}
                <input
                    type="checkbox"
                    id={course.id}
                    bind:checked={course["checked"]}
                />
                <label for={course.id}>{course.name}</label><br />
            {/each}
        </div>
        <div class="sidebar-section">
            <h3>ECEN Cores</h3>
            {#each ecenCores as course}
                <input
                    type="checkbox"
                    id={course.id}
                    bind:checked={course["checked"]}
                />
                <label for={course.id}>{course.name}</label><br />
            {/each}
        </div>
        <div class="sidebar-section">
            <h3>Electives</h3>
            <button onclick={() => (openElectives = !openElectives)}
                >Open Electives Picker</button
            >
            {#if boundElectives.length > 0}
                <h4 style="margin-top: 1em;">Selected Electives:</h4>
                {#each boundElectives as elective}
                    <div class="selected-electives">
                        <p>{elective.name}</p>
                        <button
                            onclick={() =>
                                (boundElectives = boundElectives.filter(
                                    (e) => e.id !== elective.id
                                ))}
                        >
                            <img src={trashIcon} alt="trash icon" />
                        </button>
                    </div>
                {/each}
            {/if}
        </div>
    </div>
</div>

<style>
    .sidebar {
        width: 20%;
        padding: 1em;
        box-shadow: 0 0 20px rgba(0, 0, 0, 0.3);
        margin-right: 1em;
    }

    .selected-electives {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-top: 1em;
    }

    .selected-electives p {
        margin: 0;
    }

    .selected-electives button {
        background-color: transparent;
        border: none;
        padding: 0;
        cursor: pointer;
    }

    h3 {
        margin-top: 1em;
        margin-bottom: 0.5em;
    }

    img {
        width: 1.5em;
        cursor: pointer;
        color: white;
    }
</style>
