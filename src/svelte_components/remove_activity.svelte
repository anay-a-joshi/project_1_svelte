<script>
    /*
     * Name: Anay Abhijit Joshi
     * CS 5167: User Interface 1
     * Level: Undergraduate Student
     */

    export let wantsToRemove = false;
    export let activityToRemove = '';

    // Function to handle activity removal and show alert
    const handleRemoveActivity = () => {
        if (wantsToRemove && activityToRemove.trim() !== '') {
            alert(`Verification pending!\nThe Customer Service Team has been notified to remove the following activity from your account: "${activityToRemove}".\n\nThank you for your patience! 🙏`);
            // Additional logic for removal can go here
        }
    };
</script>

<div class="remove-activity">
    <h3>Do you want to remove an activity?</h3>

    <div class="yes-no-buttons">
        <label>
            <input type="radio" bind:group={wantsToRemove} value={true}> Yes
        </label>
        <label>
            <input type="radio" bind:group={wantsToRemove} value={false}> No
        </label>
    </div>

    {#if wantsToRemove}
        <div class="remove-activity-entry">
            <label for="remove-activity">Please enter the activity you want to remove:</label>
            <input type="text" id="remove-activity" bind:value={activityToRemove} placeholder="Type the activity name...">
        </div>

        <!-- Submit button for removing activity -->
        <button on:click={handleRemoveActivity} class="submit-button">
            Submit Activity Removal Request
        </button>
    {/if}
</div>

<style>
    .remove-activity {
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

    /* Text input for removing activity */
    .remove-activity-entry {
        margin-top: 1rem;
    }

    .remove-activity-entry label {
        display: block;
        margin-bottom: 0.5rem;
    }

    .remove-activity-entry input[type="text"] {
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
        background-color: #00FF33;
        color: black;
    }
</style>
