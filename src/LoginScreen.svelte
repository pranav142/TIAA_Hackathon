<script>
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();
  let userId = '';
  let password = '';

  const handleLogin = () => {
    console.log('Logging in', { userId, password });
    dispatch('login');
  };

  const handleCreateAccount = () => {
    console.log('Redirect to create account page');
    dispatch('enter');
  };
</script>

<style>
:global(body) {
	background: linear-gradient(to top, rgb(20, 2, 2), rgb(105, 23, 23));
    background-attachment: fixed;
}

.title {
  position: absolute;
  top: 100px; /* Keep the title 100px from the top */
  left: 50%; /* Center the title horizontally */
  transform: translateX(-50%); /* Shift it back by half its own width */
  color: black;
  font-size: 50px;
  font-weight: bold;
  font-style: italic;
  background-image: url('/Investify logo png.png'); /* Add your image path here */
  background-size: cover; /* Cover the entire area of the title */
  background-position: center; /* Center the background image */
  width: 100%; /* You might need to adjust this depending on how you want your image to be displayed */
  height: 200px; /* Adjust the height as needed */
  display: block; /* Makes it a block-level element so width and height are applied */
  text-align: center; /* Centers the text horizontally */
  padding: 20px; /* Adjust padding as needed */
}


.login-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh; /* Use full height of the viewport */
}

.login-field {
  margin-bottom: 1rem;
}

.login-field input {
  color: rgb(0,0,0);
  padding: 0.5rem;
  font-size: 1rem;
  width: 250px; /* Set the width of the text fields */
  border-radius: 20px;
}

.login-button {
  color: rgb(100,0,100);
  padding: 0.5rem 1rem;
  font-size: 1rem;
  margin-bottom: 1rem;
  cursor: pointer;
  border-radius: 20px;
  border: none;
}

.login-button:hover {
  color: white;
  background-color: rgb(100,0,100);
  transition: background-color 0.125s, color 0.125s;
}
</style>

<div class="title">Investify</div>
<div class="login-container">
  <div class="login-field">
    <input
      type="text"
      placeholder="User ID"
      bind:value={userId}
    />
  </div>
  <div class="login-field">
    <input
      type="password"
      placeholder="Password"
      bind:value={password}
    />
  </div>
  <button class="login-button" on:click={handleLogin}>
    Log In
  </button>
  <button class="login-button" on:click={handleCreateAccount}>
    Create Account
  </button>
</div>