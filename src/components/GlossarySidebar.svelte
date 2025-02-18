<script>
    import csenClasses from "../assets/csenClasses.json";

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
                <p>Selected Electives:</p>
                {#each boundElectives as elective}
                    <p>{elective.name}</p>
                {/each}
            {/if}
        </div>
    </div>
</div>

<style>
    .sidebar {
        width: 20%;
        padding: 1rem;
        box-shadow: 0 0 20px rgba(0, 0, 0, 0.3);
        margin-right: 1rem;
    }
    h3 {
        margin-top: 1rem;
        margin-bottom: 0.5rem;
    }
</style>
