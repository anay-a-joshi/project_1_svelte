<script>
    /*
     * Name: Anay Abhijit Joshi
     * CS 5167: User Interface 1
     * Level: Undergraduate Student
     */

    export let wantsToLogMore;
    export let newActivity = '';

    // Function to handle submission and show alert
    const handleActivitySubmission = () => {
        if (wantsToLogMore && newActivity.trim() !== '') {
            alert(`Thanks for your patience! 🙏\nYour Add New-Activity Request has been sent to the Customer Service team. Your account would be updated soon with the new activity - '${newActivity}'.`);
            // You can add any other logic here for the submission
        }
    };
</script>

<div class="log-more">
    <h3>Do you want to log any other new activity?</h3>

    <div class="yes-no-buttons">
        <label>
            <input type="radio" bind:group={wantsToLogMore} value={true}> Yes
        </label>
        <label>
            <input type="radio" bind:group={wantsToLogMore} value={false}> No
        </label>
    </div>

    {#if wantsToLogMore}
        <div class="new-activity-entry">
            <label for="new-activity">Please enter your new activity:</label>
            <input type="text" id="new-activity" bind:value={newActivity} placeholder="Type your new activity here...">
        </div>

        <!-- Submit button that triggers the alert when the user enters the activity -->
        <button on:click={handleActivitySubmission} class="submit-button">
            Submit New-Activity Request
        </button>
    {/if}
</div>

<style>
    .log-more {
        margin-bottom: 1.5rem;
    }

    /* Flexbox for evenly spaced Yes/No buttons */
    .yes-no-buttons {
        display: flex;
        justify-content: space-between;
        margin: 1rem 0;
    }

    .yes-no-buttons label {
        flex: 1;
        text-align: center;
        margin: 0 5px;
        cursor: pointer;
        background-color: var(--primary-color);
        padding: 0.5rem;
        border-radius: 8px;
        color: white;
        transition: background 0.3s ease;
    }

    .yes-no-buttons label:hover {
        background-color: var(--primary-color-dark);
    }

    /* New activity text entry */
    .new-activity-entry {
        margin-top: 1rem;
    }

    .new-activity-entry label {
        display: block;
        margin-bottom: 0.5rem;
    }

    .new-activity-entry input[type="text"] {
        width: 100%;
        padding: 0.5rem;
        border: 1px solid #ccc;
        border-radius: 4px;
    }

    /* Style for submit button */
    .submit-button {
        margin-top: 1rem;
        padding: 0.5rem 1rem;
        background-color: blue;
        border: none;
        color: white;
        border-radius: 5px;
        cursor: pointer;
        transition: background 0.3s ease;
    }

    .submit-button:hover {
        background-color: var(--primary-color-dark);
    }
</style>
