<script>
	import Step from './components/step.svelte';
  import LoginComponent from "./components/login.svelte";
  import Navbar from "./components/navbar.svelte";
  import Todo from "./components/todo.svelte";
  import Mood from "./components/mood.svelte";
  import Sleep from "./components/sleep.svelte";
  import Heart from "./components/heart.svelte";
  import Calorie from './components/calorie.svelte';
  
  // let isAuthenticated = false;
  // let user = null;

  let isAuthenticated = true; // Set to true by default for development
  let user = { Name: "Developer" }; // Set a default user object for development

  const handleLogin = (event) => {
    isAuthenticated = true;
    user = event.detail;
  };
</script>

<!-- <div class="app-wrapper"> -->
  <!-- Navbar at the top of the page -->
  {#if isAuthenticated}
  <Navbar {isAuthenticated} />
    <div class="grid">
      <!-- Show Navbar only if authenticated -->
      <Todo />
      <Mood />
      <Sleep />
      <Heart />
      <Step />
      <Calorie />
    </div>
  {/if}

  <div class="app-container">
    {#if !isAuthenticated}
      <div class="left-half">
        <LoginComponent on:login={handleLogin} />
      </div>
      <div class="right-half"></div>
    {/if}
  </div>
<!-- </div> -->

<style>
  .app-container {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    color: black;
    font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  }

  .left-half {
    flex: 1;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 2rem;
  }

  .right-half {
    flex: 1;
    height: 100vh; /* Make sure it takes full viewport height */
    background-image: url("/ibgr.jpg"); /* Ensure this path is correct */
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
  }

  .welcome-message {
    margin-top: 2rem;
    font-size: 1.5rem;
    text-align: center;
  }

  /* .app-wrapper {
    display: flex;
    flex-direction: column;
    height: 100vh;
  } */

  .app-container {
    flex: 1;
    display: flex;
  }
  .grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr); /* 3 columns */
    grid-template-rows: repeat(2, auto); /* 2 rows */
    gap: 1rem; /* Space between items */
    padding: 0%;  
    justify-items: center
  }

  /* object-fit: cover; */
</style>
