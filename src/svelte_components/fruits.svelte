<script>
    /*
     * Name: Anay Abhijit Joshi
     * CS 5167: User Interface 1
     * Level: Undergraduate Student
     */

    import { tweened } from 'svelte/motion';
    import { cubicOut } from 'svelte/easing';

    const progress = tweened(0, {
        duration: 400,
        easing: cubicOut
    });

    // Add an array to store the selected fruits
    let selectedFruits = [];

    export let fruitIntake = 0; // Add this to handle two-way binding for fruits

    // Function to update the fruit intake and add to selected fruits
    function selectFruit(fruit) {
        if (!selectedFruits.includes(fruit)) {
            selectedFruits = [...selectedFruits, fruit]; // Add the fruit if not already selected
            fruitIntake = selectedFruits.length; // Update the intake count
            progress.set(fruitIntake / 6);  // Update the progress bar (assuming max 6 servings)
        }
    }

    // Function to remove a fruit
    function removeFruit(fruit) {
        selectedFruits = selectedFruits.filter(f => f !== fruit);
        fruitIntake = selectedFruits.length;
        progress.set(fruitIntake / 6);
    }
</script>

<div class="fruit-intake">
    <h3>Track Your Fruit Intake for Today</h3>
    <progress value={$progress} max="1"></progress>

    <div class="fruit-buttons">
        <button on:click={() => selectFruit('Apple 🍎')}>Apple 🍎</button>
        <button on:click={() => selectFruit('Banana 🍌')}>Banana 🍌</button>
        <button on:click={() => selectFruit('Mango 🥭')}>Mango 🥭</button>
        <button on:click={() => selectFruit('Watermelon 🍉')}>Watermelon 🍉</button>
        <button on:click={() => selectFruit('Strawberry 🍓')}>Strawberry 🍓</button>
        <button on:click={() => selectFruit('Grapes 🍇')}>Grapes 🍇</button>
    </div>

    <!-- Display the selected fruits -->
    {#if selectedFruits.length > 0}
        <div class="selected-fruits">
            <h4>Selected Fruits:</h4>
            <ul>
                {#each selectedFruits as fruit}
                    <li>{fruit} <button on:click={() => removeFruit(fruit)}>Remove</button></li>
                {/each}
            </ul>
        </div>
    {/if}
</div>

<style>
    .fruit-buttons {
        display: flex;
        justify-content: space-between;
        margin-top: 1rem;
    }

    .fruit-buttons button {
        flex: 1; 
        margin: 0 10px;
        padding: 0.5rem;
        border: none;
        border-radius: 8px;
        cursor: pointer;
        background-color: var(--primary-color);
        color: white;
        transition: background 0.3s ease;
    }

    .fruit-buttons button:hover {
        background-color: var(--primary-color-dark);
    }

    .selected-fruits {
        margin-top: 1rem;
    }

    .selected-fruits ul {
        list-style-type: none;
        padding: 0;
    }

    .selected-fruits li {
        display: flex;
        justify-content: space-between;
        margin: 5px 0;
        padding: 5px;
        background-color: #f9f9f9;
        border-radius: 5px;
        border: 1px solid #ddd;
    }

    .selected-fruits button {
        background-color: blue;
        color: white;
        border: none;
        padding: 0.3rem 0.5rem;
        border-radius: 4px;
        cursor: pointer;
    }

    .selected-fruits button:hover {
        background-color: #00FF33;
        color: black;
    }
</style>
