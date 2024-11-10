<script>
  import { createEventDispatcher } from 'svelte';

  let username = "";
  let password = "";
  let rememberMe = false;
  let isLogin = true;
  let Name = "";

  const dispatch = createEventDispatcher();

  const handleLogin = () => {
    const storedUser = JSON.parse(localStorage.getItem(username));
    if (storedUser && storedUser.password === password) {
      alert(`Welcome back, ${storedUser.Name}!`);
      dispatch('login', { username, Name: storedUser.Name });
    } else {
      alert('Invalid username or password.');
    }
  };

  const handleSignUp = () => {
    const storedUser = JSON.parse(localStorage.getItem(username));
    if (storedUser) {
      alert('User already exists. Please login.');
    } else {
      const newUser = { username, password, Name };
      localStorage.setItem(username, JSON.stringify(newUser));
      alert('Account created! Please login.');
      isLogin = true;
    }
  };

  const handleSubmit = () => {
    if (isLogin) {
      handleLogin();
    } else {
      handleSignUp();
    }
  };

  const toggleMode = () => {
    isLogin = !isLogin;
  };
</script>

<style>
  .login-container {
    background-color: #f5f5f5;
    padding: 2rem;
    border-radius: 10px;
    box-shadow: 0px 5px 15px rgba(0, 0, 0, 0.3);
    max-width: 400px;
    width: 100%;
    text-align: center;
    margin-left: 0;
  }

  .welcome-title {
    font-size: 1.8rem;
    color: #927357;
    margin-bottom: 0.5rem;
  }

  .welcome-quote {
    font-size: 1rem;
    color: #555;
    margin-bottom: 1.5rem;
    font-style: italic;
  }

  .login-title {
    font-size: 1.5rem;
    margin-bottom: 1rem;
    color: #937457;
  }

  .input-field {
    width: 100%;
    padding: 0.8rem;
    margin-bottom: 1rem;
    border: 1px solid #ccc;
    border-radius: 5px;
  }

  .checkbox-container {
    display: flex;
    align-items: center;
    margin-bottom: 1.5rem;
  }

  .checkbox-container input {
    margin-right: 0.5rem;
  }

  .login-button {
    width: 100%;
    padding: 0.8rem;
    border: none;
    background-color: #dfaf8b; 
    color: #fff;
    border-radius: 5px;
    cursor: pointer;
    font-weight: bold;
  }

  .login-button:hover {
    background-color: #937457;
  }

  .toggle-button {
    width: 100%;
    padding: 0.5rem;
    border: none;
    background-color: #f0f0f0;
    color: #333;
    border-radius: 5px;
    cursor: pointer;
    font-weight: bold;
    margin-top: 1rem;
  }

  .toggle-button:hover {
    background-color: #e0e0e0;
  }
</style>

<div class="login-container">
  <h1 class="welcome-title">Welcome to PulsePath</h1>
  <p class="welcome-quote">"Great journeys begin with small steps. Let’s make today count!"</p>
  
  <h2 class="login-title">{isLogin ? 'Login' : 'Sign Up'}</h2>
  
  <input
    class="input-field"
    type="text"
    placeholder="Username"
    bind:value={username}
  />
  {#if !isLogin}
    <input
      class="input-field"
      type="text"
      placeholder="Name"
      bind:value={Name}
    />
  {/if}
  <input
    class="input-field"
    type="password"
    placeholder="Password"
    bind:value={password}
  />
  {#if isLogin}
    <div class="checkbox-container">
      <input id="rememberMe" type="checkbox" bind:checked={rememberMe} />
      <label for="rememberMe">Remember me</label>
    </div>
  {/if}
  <button class="login-button" on:click={handleSubmit}>{isLogin ? 'Login' : 'Sign Up'}</button>
  <button class="toggle-button" on:click={toggleMode}>{isLogin ? 'Need an account? Sign Up' : 'Have an account? Login'}</button>
</div>
