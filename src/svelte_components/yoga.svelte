<script>

    /*
     * Name: Anay Abhijit Joshi
     * CS 5167: User Interface 1
     * Level: Undergraduate Student
     */

    export let didYoga;
    export let yogaDuration;
</script>

<div class="yoga-duration">
    <h3>Did you manage to fit in some yoga today?</h3>

    <div class="yes-no-buttons">
        <label>
            <input type="radio" bind:group={didYoga} value={true}> Yes
        </label>
        <label>
            <input type="radio" bind:group={didYoga} value={false}> No
        </label>
    </div>

    {#if didYoga}
        <div class="yoga-slider">
            <label for="yoga">How long did you practice yoga today? (Minutes):</label>
            <input type="range" id="yoga" bind:value={yogaDuration} min="0" max="100" step="5" style="width: 80%">
            <p>Great job! You've completed {yogaDuration} minutes of yoga today.</p>
        </div>
    {/if}
</div>

<style>
    .yoga-duration {
        margin-bottom: 1.5rem;
    }

    /* Flexbox for evenly spaced Yes/No buttons */
    .yes-no-buttons {
        display: flex;
        justify-content: space-between; /* Evenly space Yes and No buttons */
        margin: 1rem 0; /* Optional margin for spacing */
    }

    .yes-no-buttons label {
        flex: 1; /* Make Yes and No labels take equal space */
        text-align: center; /* Center the text inside the label */
        margin: 0 5px; /* Add some space between buttons */
        cursor: pointer; /* Make the label act like a button */
        background-color: var(--primary-color);
        padding: 0.5rem;
        border-radius: 8px;
        color: white;
        transition: background 0.3s ease;
    }

    .yes-no-buttons label:hover {
        background-color: var(--primary-color-dark);
    }

    /* For the yoga slider */
    .yoga-slider {
        margin-top: 1rem;
    }

    .yoga-slider label {
        display: block;
        margin-bottom: 0.5rem;
    }

    .yoga-slider input[type="range"] {
        width: 100%;
    }
</style>
