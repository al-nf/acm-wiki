<script>
    import pastMeetings from "../assets/pastMeetings.json";
    import { onMount } from "svelte";
    import MeetingCard from "../components/MeetingCard.svelte";
    import Select from "svelte-select";

    let meetings = $state([]);
    let filteredMeetings = $state([]);
    let event = $state("");
    let quart = $state("");
    let year = $state(0);

    let eventTypes = [
        {value: 'Technical Workshop', label: 'Technical Workshop'},
        {value: 'Career Development', label: 'Career Development'},
        {value: 'Hackathon Prep', label: 'Hackathon Prep'},
        {value: 'General Event', label: 'General Event'},
    ];
    let quarters = [
        {value: 'Fall', label: 'Fall'},
        {value: 'Winter', label: 'Winter'},
        {value: 'Spring', label: 'Spring'}
    ];
    let years = [
        {value: 2024, label: '2024'},
        {value: 2023, label: '2023'}
    ];

    function getMeetings(){
        meetings = pastMeetings.map((m) => ({
            data: {
                id: m.id,
                name: m.name,
                link: m.link,
                event: m.event,
                year: m.year,
                quarter: m.quarter,
            },
        }));
    }

    onMount(() => {
        getMeetings();
        filteredMeetings = [...meetings];
    })

    $effect(() => {
        filteredMeetings = [...meetings.filter((m) => {
            return (event.length == 0 || m.data.event == event) && (quart.length == 0 || m.data.quarter == quart) && (year == 0 || m.data.year == year);
        })]
    })

</script>

<main>
    <h1>Past ACM Meetings</h1>
    <div class="filters">
        <div class="fil">
            <Select
            placeholder={"Filter by event type"}
            --width="100%"
            --background="transparent"
            --list-background="#13171f"
            --item-hover-bg="#24272e"
            items={eventTypes} on:input={(e) => event = e.detail.value} on:clear={() => event = ""}/>
        </div>
        <div class="fil">
            <Select
            placeholder={"Filter by quarter"}
            --background="transparent"
            --list-background="#13171f"
            --item-hover-bg="#24272e"
            items={quarters} on:input={(e) => quart = e.detail.value} on:clear={() => quart = ""}/>
        </div>
        <div class="fil">
            <Select
            placeholder={"Filter by year"}
            --background="transparent"
            --list-background="#13171f"
            --item-hover-bg="#24272e"
            items={years} on:input={(e) => year = e.detail.value} on:clear={() => year = 0}/>
        </div>
    </div>
    
    {#each filteredMeetings as m}
        {#if m}
            <MeetingCard 
                name={m.data.name}
                slides={m.data.link} 
                event={m.data.event}
                year={m.data.year}
                quarter={m.data.quarter}/>
        {/if}
    {/each}
</main>

<style>
    div.filters {
        display: flex;
        width: 100%;
        /* flex-direction: column; */
        gap: 1em;
    }
    div.fil {
        width: calc(100%/3);
    }
    @media (max-width: 576px) {
        div.filters {
            display: block;
        }
        div.fil {
            width: 100%;
            padding-bottom: 1em;
        }
    }
</style>