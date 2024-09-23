<script lang="ts">
    import { createEventDispatcher } from 'svelte';
    
    let username = '';
    let password = '';
    let isLogin = true;  // Toggle between login and sign-up
    const dispatch = createEventDispatcher(); // Create dispatcher to send login event

    // Function to handle login
    const handleLogin = () => {
        const storedUser = JSON.parse(localStorage.getItem(username));
        
        if (storedUser && storedUser.password === password) {
            alert(`Welcome back, ${username}!`);
            dispatch('login', { username });
        } else {
            alert('Error! Invalid login details, please try again or create an account!');
        }
    };

    // Function to handle sign-up
    const handleSignUp = () => {
        const storedUser = JSON.parse(localStorage.getItem(username));

        if (storedUser) {
            alert('User already exists. Please login.');
        } else {
            const newUser = { username, password};
            localStorage.setItem(username, JSON.stringify(newUser));
            alert('Success! Your account has been created! Please login again with the valid credentials.');
            isLogin = true;
        }
    };

    // Function to handle form submission based on mode
    const handleSubmit = () => {
        if (isLogin) {
            handleLogin();
        } else {
            handleSignUp();
        }
    };

    // Toggle between Login and Sign-Up
    const toggleMode = () => {
        isLogin = !isLogin;
    };

    const quotes = [
        "Your health is your wealth.",
        "A healthy outside starts from the inside.",
        "Take care of your body, it's the only place you have to live.",
        "Health is not about the weight you lose but the life you gain.",
        "To get rich, never risk your health. For it is the truth that health is the wealth of wealth.",
        "It is Health that is Real Wealth, and Not Pieces of Gold and Silver"
    ];

    let randomQuote = quotes[Math.floor(Math.random() * quotes.length)];
</script>

<style>
    .login-container {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 100vh;
        background-color: aqua;
        font-family: 'Roboto', sans-serif;
        padding: 1rem;
    }

    .header {
        font-size: 3rem;
        color: red; /* Blue-gray color for the main text */
        margin-bottom: 1rem;
        text-align: center;
        font-weight: 600;
        text-transform: uppercase;
        position: relative;
        text-shadow: 2px 2px 0 #333,   /* First layer shadow */
                    4px 4px 0 #555,   /* Second layer shadow */
                    6px 6px 0 #777;   /* Third layer shadow */
    }

    .header::before {
        content: "Fitness Spectrum";
        position: absolute;
        top: 3px;
        left: 3px;
        color: #F0F0F0;  /* Light gray for the raised highlight effect */
        z-index: -1;
        text-shadow: none;
    }


    .quote-box {
        background-color: red;
        border-radius: 8px;
        padding: 2rem;
        font-size: 1.4rem;
        color: ghostwhite;
        margin-bottom: 2rem;
        text-align: center;
        border: 1px solid #e0e0e0;
        box-shadow: 0 10px 15px rgba(0, 0, 0, 0.05);
    }

    .login-box {
        padding: 3rem;
        border-radius: 12px;
        box-shadow: 0 15px 30px rgba(0, 0, 0, 0.1);
        background-color: #ffffff;
        max-width: 450px;
        width: 100%;
        text-align: center;
    }

    input {
        margin: 1rem 0;
        padding: 1rem;
        width: 100%;
        border-radius: 8px;
        border: 1px solid #ddd;
        font-size: 1.1rem;
        transition: all 0.3s ease;
    }

    input:focus {
        outline: none;
        border-color: #00796b;
        box-shadow: 0 0 5px rgba(0, 121, 107, 0.2);
    }

    .button {
    margin-top: 2rem;
    padding: 1rem;
    border: none;
    border-radius: 8px;
    background: linear-gradient(135deg, #3a8dff, #00796b); /* Gradient from blue to teal */
    color: white;
    font-size: 1.2rem;
    font-weight: bold;
    cursor: pointer;
    width: 100%;
    transition: background 0.3s ease, transform 0.2s ease;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1); /* Soft shadow for depth */
    }

    button:hover {
        background: linear-gradient(135deg, #00796b, #3a8dff); /* Reverse gradient on hover */
        transform: translateY(-2px); /* Slight lift on hover */
    }

    button:active {
        transform: translateY(0); /* Reset on click */
        box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2); /* Deeper shadow when pressed */
    }


    .toggle-button {
        margin-top: 1rem;
        background-color: transparent;
        color: #00796b;
        border: none;
        cursor: pointer;
        font-size: 1rem;
        transition: color 0.3s ease;
    }

    .toggle-button:hover {
        color: #004d40;
    }

    @media (max-width: 600px) {
        .login-box {
            padding: 2rem;
        }

        .header {
            font-size: 2rem;
        }
    }
</style>

<div class="login-container">
    <div class="header"> Fitness Spectrum </div>

    <div class="login-box">
        <h2>{isLogin ? 'Welcome Back!' : 'Create Your Account'}</h2>
        <input type="text" bind:value={username} placeholder="Enter Your Name" />
        <input type="password" bind:value={password} placeholder="Enter Your Password" />
        <button on:click={handleSubmit}>{isLogin ? 'Login Now' : 'Sign Up Now'}</button>
        <button class="toggle-button" on:click={toggleMode}>
            {isLogin ? "New here? Create an account" : 'Already a user? Log in'}
        </button>
    </div>


    <div class="quote-box" style="margin-top: 2rem;">
        <p>"{randomQuote}"</p>
    </div>
</div>