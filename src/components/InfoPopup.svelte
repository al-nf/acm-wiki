<script>
    let { openInfo = $bindable(true) } = $props();
</script>

<div class="popup">
    <div class="popup-content">
        <button class="close-button" onclick={() => (openInfo = !openInfo)}
            >x</button
        >
        <div class="info">
            <h2>ACM Wiki CSEN Glossary Tutorial</h2>
            <p>
                <strong>
                    The goal of the glossary is to give you an idea on how to
                    plan your classes and explore the options available to you.
                    This can be done in several ways:
                </strong>
            </p>
            <p>
                <strong>Course Roadmap Graph:</strong> You can view all of the classes
                you have to take in order to graduate sorted by year and quarter.
                You can remove classes you've already taken by checking their boxes.
                Red lines indicate the prerequisites tree for a course. Click on
                a node to see more information about the course, including what quarters
                it is being offered and who is teaching it.
            </p>
            <p>
                <strong>Elective Explorer:</strong> You can view all of the electives
                available to you and choose which ones you want to take. Along with
                when the course is offered, there is also insight from ACM board
                members that have taken the course before.
            </p>
            <p>
                <strong>Works great with SCU Schedule:</strong> Once you've
                settled on a 4-year plan that works for you, you can use SCU
                Schedule, another ACM maintained tool, to plan out your schedule
                for the current quarter, which includes all classes offered, not
                just CSEN classes. Check that out
                <a href="https://scuschedule.com" target="_blank">here</a>.
            </p>
            <p>
                <strong>Note:</strong> The information provided is not
                guaranteed to be accurate. The information for this is pulled
                from Professor Atkinson's list
                <a
                    href="https://www.cse.scu.edu/~datkinson/info/"
                    target="_blank">here</a
                >, which is subject to change Please consult with your academic
                advisor before making any decisions.
            </p>
            <p>
                <strong>Questions or comments?</strong> Email
                <a href="mailto:acm@scu.edu">acm@scu.edu</a>
            </p>
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
        width: 60%;
        height: 60%;
        position: relative;
    }

    .close-button {
        position: absolute;
        right: 1em;
        top: 1em;
        background-color: transparent;
        border: none;
        color: white;
        font-size: 1.5em;
    }

    .info {
        padding: 2em;
        overflow-y: scroll;
    }

    .info::-webkit-scrollbar {
        width: 12px;
    }

    .info::-webkit-scrollbar-track {
        background: #f1f1f1;
    }

    .info::-webkit-scrollbar-thumb {
        background: #888;
        border-radius: 6px;
    }

    .info::-webkit-scrollbar-thumb:hover {
        background: #555;
    }
</style>
