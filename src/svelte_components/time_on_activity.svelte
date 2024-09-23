<script>

    /*
     * Name: Anay Abhijit Joshi
     * CS 5167: User Interface 1
     * Level: Undergraduate Student
     */

    export let skillPractice;
    export let skill;  // Receive the skill from parent component
</script>

<div class="skill-practice">
    <h3>{skill} Progress Tracker</h3>
    <label for="skill">Hours dedicated to {skill} today: </label>
    <input type="number" id="skill" bind:value={skillPractice} min="0" max="24">
</div>

<style>
    input[type="number"] {
        width: 100%;
        padding: 0.5rem;
        border: 1px solid #ddd;
        border-radius: 8px;
        margin-top: 0.25rem;
    }
</style>
