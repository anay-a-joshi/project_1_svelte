<script>

    /*
     * Name: Anay Abhijit Joshi
     * CS 5167: User Interface 1
     * Level: Undergraduate Student
     */

    export let habitProgress = 0; // Progress for each habit
    export let habitName = ''; // Name of the habit to display
</script>

<div class="progress-bar-container">
    <p>{habitName}: You've completed {habitProgress}% of your target!</p>
    <progress value={habitProgress} max="100"></progress>
</div>

<style>
    .progress-bar-container {
        margin: 1rem 0;
    }
    progress {
        width: 100%;
        height: 1rem;
        border-radius: 8px;
        overflow: hidden;
    }
    progress::-webkit-progress-bar {
        background-color: #f3f3f3;
    }
    progress::-webkit-progress-value {
        background-color: var(--primary-color);
    }
</style>
