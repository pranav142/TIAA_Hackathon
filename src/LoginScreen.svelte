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
    // This can be where you redirect to a 'create account' component or use another dispatch
  };
</script>

<style>
:global(body) {
	background: linear-gradient(to right, rgb(152,140,245), rgb(206,140,245));
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