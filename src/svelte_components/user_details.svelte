<script>

    /*
     * Name: Anay Abhijit Joshi
     * CS 5167: User Interface 1
     * Level: Undergraduate Student
     */

    export let user; 
    let currentDate = new Date(); // Current date for user information
    let startDate = new Date('2024-09-11'); // User's start date as a Date object
    let daysActive = Math.floor((currentDate.getTime() - startDate.getTime()) / (1000 * 60 * 60 * 24)); // Difference in days
</script>

<section class="user-info">
    <h1>Welcome {user.username} !</h1>
    <p>It's {currentDate.toDateString()}, and the time is {new Date().toLocaleTimeString()}.</p>
    <br>
    <p>{user.username}'s journey began with us on Sep 11, 2024.</p>
    <p class="active-days">You've been actively using the platform for {daysActive} days. Keep it going!</p>
</section>

<style>
    .user-info {
        text-align: center;
        background-color: red; /* Light background to make the text stand out */
        padding: 20px;
        border-radius: 10px; /* Soft rounded corners for a modern look */
        max-width: 400px;
        margin: 0 auto; /* Center the section */
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* Subtle shadow for depth */
        font-family: 'Arial', sans-serif; /* Clean and readable font */
    }


    .user-info h1 {
        font-size: 2rem;
        margin-bottom: 10px;
        color: black; /* Darker text for good contrast */
    }

    .user-info p {
        margin: 0.5rem 0;
        color: #f0f4c3; /* Softer text color for less emphasis */
    }


    .user-info .date, .user-info .active-days {
        font-size: 1.2rem; /* Slightly increased font size for readability */
        font-weight: 500;
        color: #333;
    }

    .user-info .date {
        font-size: 1.2rem; /* Slightly increased font size for readability */
        font-weight: 500;
        color: #333;
    }

    .user-info .active-days {
        background-color: #e0f7fa; /* Highlight active days with a soft background color */
        padding: 10px;
        border-radius: 5px;
        display: inline-block; /* Keep the highlight contained */
    }

    /* Add hover effect to improve interaction */
    .user-info h1:hover {
        color: #00796b; /* Change color on hover for interactivity */
        transition: color 0.3s ease;
    }

    .user-info .active-days:hover {
        background-color: #b2ebf2; /* Slight change on hover for active days */
        transition: background-color 0.3s ease;
    }
</style>
