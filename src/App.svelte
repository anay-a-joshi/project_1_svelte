<script>
    // Name: Anay Abhijit Joshi
    // CS 5167: User Interface 1
    // Level: Undergraduate Student

    import Login from './svelte_components/user_login.svelte';
    import Feelings from './svelte_components/daily_feelings.svelte';
    import ImageUpload from './svelte_components/daily_image.svelte';
    import Reflection from './svelte_components/journaling.svelte';
    import SkillPractice from './svelte_components/time_on_activity.svelte';
    import YogaDuration from './svelte_components/yoga.svelte';
    import UserInfo from './svelte_components/user_details.svelte';
    import WaterIntake from './svelte_components/water_consumption.svelte';
    import ProductivityChart from './svelte_components/visual_feedback.svelte';
    import Progress from './svelte_components/activity_progress.svelte';
    import LogMoreActivity from './svelte_components/new_activity.svelte'; // Import the new component
    import RemoveActivity from './svelte_components/remove_activity.svelte';

    // Your existing variables and functions
    let wantsToRemove = false;
    let activityToRemove = '';

    let wantsToLogMore = false;  // Track if user wants to log more
    let newActivity = '';        // Variable for storing the new activity input

    // Theme toggle state
    let isDarkMode = false;

    // Helper to toggle between themes
    const toggleTheme = () => {
        isDarkMode = !isDarkMode;
        document.documentElement.setAttribute('data-theme', isDarkMode ? 'dark' : 'light');
    };

    let loggedIn = false;  // Track if user is logged in
    let user = { username: '', startDate: new Date() };
    let currentDate = new Date();  // Current date for user information
    let selectedDate = new Date();  // Default is today's date
    let daysActive = 1;

    // Journal Data
    let feelings = [
    { mood: 'Joyful', description: 'Feeling lighthearted and happy', checked: false },
    { mood: 'Melancholic', description: 'A feeling of deep sadness', checked: false },
    { mood: 'Curious', description: 'Eager to learn or explore something new', checked: false },
    { mood: 'Stressed', description: 'Overwhelmed by tasks or challenges', checked: false },
    { mood: 'Serene', description: 'A peaceful and calm state of mind', checked: false },
    { mood: 'Irritated', description: 'Feeling easily annoyed or frustrated', checked: false },
    { mood: 'Appreciative', description: 'Grateful for the good things in life', checked: false },
    { mood: 'Disconnected', description: 'Feeling detached from others', checked: false },
    { mood: 'Empowered', description: 'Feeling in control and confident', checked: false },
    { mood: 'Fatigued', description: 'Tired and lacking energy', checked: false },
    { mood: 'Optimistic', description: 'Hopeful and positive about the future', checked: false },
    { mood: 'Uninspired', description: 'Lacking motivation or creativity', checked: false }
    ];

    let image = '';
    let dailyReflection = '';
    let skillPractice = 0;
    let didYoga = false;
    let yogaDuration = 0;
    let waterIntake = 0;
    let skill = '';

    // Productivity data for chart
    let productivityData = [skillPractice * 60 , yogaDuration / 60 , waterIntake * 80];

    // Progress tracking logic
    let skillPracticeGoal = 5; // Example: 60 minutes skill practice per day
    let yogaGoal = 100; // Example: 30 minutes yoga per day
    let waterGoal = 4; // Example: 2000 ml water intake per day

    let skillPracticeProgress = (skillPractice / skillPracticeGoal) * 100;
    let yogaProgress = (yogaDuration / yogaGoal) * 4;
    let waterIntakeProgress = ((waterIntake) / waterGoal) * 4;

    // Helper function to format date as YYYY-MM-DD for input value
    const formatDateForInput = (date) => {
        return date.toISOString().split('T')[0];
    };

    // Handle login success and retrieve stored data
    const onLoginSuccess = (event) => {
        user.username = event.detail.username;  // Assign username after login
        loggedIn = true;
        retrieveJournalData();  

        setTimeout(() => {
            skill = prompt(`Hi ${user.username}, what specific skill would you like to focus on improving today? 🤔`) || 'Skill';  // Fallback to 'Skill' if input is empty
    }, 100);
    };

    // Update journal data based on selected date
    const onDateChange = (event) => {
        selectedDate = new Date(event.target.value);
        retrieveJournalData();  // Load journal data for the newly selected date
    };

    // Save journal data in localStorage for the selected date
    const saveJournalData = () => {
        const journalData = {
            feelings,
            image,
            dailyReflection,
            skillPractice,
            didYoga,
            yogaDuration,
            waterIntake,
            wantsToLogMore,      // Include the decision to log more
            newActivity
        };

        // Store the data in localStorage with the user's name and the selected date as key

        const formattedDate = selectedDate.toISOString().split("T")[0];
        localStorage.setItem(user.username + '_journal_' + formattedDate, JSON.stringify(journalData));

        // Update productivityData for the pie chart
        productivityData = [skillPractice, yogaDuration / 60, waterIntake];

        // Update progress tracking
        skillPracticeProgress = (skillPractice / skillPracticeGoal) * 100;
        yogaProgress = (yogaDuration / yogaGoal) * 100;
        waterIntakeProgress = (waterIntake / waterGoal) * 100;

        alert('✅ Success! \nJournal saved for ' + formattedDate + '!');
    };

    // Retrieve journal data from localStorage and populate the fields for the selected date
    const retrieveJournalData = () => {
        const formattedDate = selectedDate.toISOString().split("T")[0];
        const savedJournalData = localStorage.getItem(user.username + '_journal_' + formattedDate);

        if (savedJournalData) {
            const journalData = JSON.parse(savedJournalData);

            // Restore all fields with the saved data
            feelings = journalData.feelings || feelings;
            image = journalData.image || '';
            dailyReflection = journalData.dailyReflection || '';
            skillPractice = journalData.skillPractice || 0;
            didYoga = journalData.didYoga || false;
            yogaDuration = journalData.yogaDuration || 0;
            waterIntake = journalData.waterIntake || 0;

            // Update productivityData for the pie chart
            productivityData = [skillPractice, yogaDuration/60, waterIntake];

            // Update progress tracking
            skillPracticeProgress = (skillPractice / skillPracticeGoal) * 100;
            yogaProgress = (yogaDuration / yogaGoal) * 100;
            waterIntakeProgress = (waterIntake / waterGoal);
        } else {
            // If no data for the selected date, reset the fields
            feelings.forEach(feeling => feeling.checked = false);
            image = '';
            dailyReflection = '';
            skillPractice = 0;
            didYoga = false;
            yogaDuration = 0;
            waterIntake = 0;

            // Reset productivityData
            productivityData = [0, 0, 0];

            // Reset progress tracking
            skillPracticeProgress = 0;
            yogaProgress = 0;
            waterIntakeProgress = 0;

        }
    };

    const handleJournalFetch = () => {
    const formattedDate = selectedDate.toISOString().split('T')[0];  // Format as YYYY-MM-DD
        const savedJournalData = localStorage.getItem(user.username + '_journal_' + formattedDate);

        if (savedJournalData) {
            retrieveJournalData();  // Fetch and populate journal data if it exists
            alert(`✅ Great! \nYour data entry for ${formattedDate} has been loaded successfully.`);
        } else {
            alert(`🥺 Oops! \nYou haven't logged any activity for ${formattedDate} yet. Please fill in your details to get started!`);  // Show alert if no data found
        }
    };

</script>

<main>

    <section class="theme-toggle">
        <button class="theme-toggle-button" on:click={toggleTheme}>
            {#if isDarkMode}
            🌝 Light Mode
            {/if}
            {#if !isDarkMode}
            🌚 Dark Mode
            {/if}
        </button>
    </section>

    {#if loggedIn}

        <section class=" card user-info-section">
            <h2>{user.username}'s Details </h2>
            <UserInfo {user}  />
        </section>

        <!-- Date picker to select the date for the journal -->
        <section class="card date-picker-section">
            <h2>Pick the Date</h2>
            <div class="date-picker">
                <label for="journal-date">Calendar Date:</label>
                <input type="date" id="journal-date" value={formatDateForInput(selectedDate)} on:change={onDateChange}>

            <!-- Button to fetch data for the selected date -->
            <button on:click={handleJournalFetch} class="fetch-button">Fetch Previous Entry</button>
            </div>
        </section>

        <section class="card feelings-section">
            <h2>{user.username}'s Mood/Feelings</h2>
            <Feelings {feelings} />
        </section>

        <section class="card image-upload-section">
            <h2>Image of the Day (Please Upload)</h2>
            <ImageUpload bind:image />
        </section>

        <section class="card goal-section">
            <h2>Goals/Targets</h2>
            <form>
                <label for="skillPracticeGoal">Time Spent on {skill} (Hours) by {user.username}:</label>
                <input type="number" id="skillPracticeGoal" bind:value={skillPracticeGoal} min="1">

                <label for="yogaGoal">{user.username}'s Yoga/Stretching Duration (Minutes):</label>
                <input type="number" id="yogaGoal" bind:value={yogaGoal} min="1">

                <label for="waterGoal">{user.username}'s Body Hydration Goal (Liters):</label>
                <input type="number" id="waterGoal" bind:value={waterGoal} step="0.1" min="0.1">
            </form>
        </section>

        <section class="card reflection-section">
            <h2>Today's Insights of {user.username}</h2>
            <Reflection bind:dailyReflection />
        </section>

        <section class="card skill-practice-section">
            <h2>{skill}</h2>
            <SkillPractice bind:skillPractice {skill} />
        </section>

        <section class="card yoga-section">
            <h2>{user.username}'s Yoga/Stretching</h2>
            <YogaDuration bind:didYoga bind:yogaDuration />
        </section>

        <section class="card water-intake-section">
            <h2>{user.username}'s Body Hydration</h2>
            <WaterIntake bind:waterIntake />
        </section>

        <section class="card log-more-section">
            <h2>Add New Activity Request</h2>
            <LogMoreActivity bind:wantsToLogMore bind:newActivity />
        </section>

        <section class="card remove-activity-section">
            <h2>Remove Activity Request</h2>
            <RemoveActivity bind:wantsToRemove bind:activityToRemove />
        </section>

        <!-- Submit button to save journal data -->
        <button on:click={saveJournalData} class='submit'>Submit</button>

        <!-- Progress tracking for habits -->
        <section class="card progress-tracking-section">
            <h2>{user.username}'s Overall Average (in %)</h2>
            <Progress habitProgress={skillPracticeProgress} habitName="Average Time on {skill}" />
            <Progress habitProgress={yogaProgress} habitName="Average Stretching Duration" />
            <Progress habitProgress={waterIntakeProgress} habitName="Average Water Intake" />
        </section>

        <!-- Productivity Pie Chart -->
        <section class="card productivity-chart-section">
            <h2>{user.username}'s Efficiency Overview</h2>
            <ProductivityChart {productivityData} />
        </section>

    {/if}

    {#if !loggedIn}
        <!-- Show login if user is not logged in -->
        <Login on:login={onLoginSuccess} />
    {/if}
</main>

