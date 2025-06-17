<script>
    import { onMount } from "svelte";
    import {Link} from 'svelte-routing';

    onMount(() => {
        document.title = "SCU ACM Wiki";
    });
</script>

<main>
    <h1>Welcome to the SCU ACM Wiki!</h1>
    <p>
        Here you can find all kinds of resources curated by ACM by SCM for
        academics, career, and technical development.
    </p>
    <div class="cardRow">
        <div class="card">
            <Link to="/academics">
            <h3>Academics</h3>
            <p class="desc">Need help with figuring out your four-year plan? Confused over which professors to take or what requirements there are? Take look at our glossary and guides!</p>
            </Link>
        </div>
        <div class="card">
            <Link to="/tutorials">
                <h3>Tutorials</h3>
                <p class="desc">Seeking to sharpen your technical skills and learn something new? Look no further than ACM's tutorials, where you can pick up a new language or become familiar with a new framework!</p>
            </Link>
        </div>
    </div>
    <div class="cardRow">
        <div class="card">
            <Link to="/career">
                <h3>Career</h3>
                <p class="desc">Getting an internship can be tough in today's job market. Our career guides give you helpful advice on your resume, interviews, networking, and more!</p>
            </Link>
        </div>
        <div class="card">
            <Link to="/acmhistory">
                <h3>ACM History</h3>
                <p class="desc">Attended one of your events and missed something important on the slides? Or just curious about what ACM taught in previous years? All our past meetings slides are available right here. </p>
            </Link>
        </div>
    </div>
</main>

<style>
    div.card {
        text-align: center;
        padding: 1em;
        height: auto;
        align-content: center;
        align-items: center;
        margin: 1rem;
        box-shadow: 0px 0px 5px gray;
        border-radius: 20px;
        flex: 1;
    }
    div.card:hover * {
        color: aqua;
    }
    p.desc {
        color:rgb(194, 199, 208);
        text-decoration: none;
    }
    div.cardRow {
        display: flex;
        flex-direction: row;
    }
    @media (max-width: 576px) {
        div.cardRow {
            display: block;
            flex-direction: none;
        }
        div.card {
            width: 100%;
        }
    }
</style>
