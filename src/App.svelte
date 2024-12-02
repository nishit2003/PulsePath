<script>
	import Step from './components/step.svelte';
  // @ts-ignore
  import LoginComponent from "./components/login.svelte";
  import Navbar from "./components/navbar.svelte";
  import Todo from "./components/todo.svelte";
  import Mood from "./components/mood.svelte";
  import Sleep from "./components/sleep.svelte";
  import Heart from "./components/heart.svelte";
  import Calorie from './components/calorie.svelte';
  import Footer from './components/footer.svelte';
  import Hero from './components/hero.svelte';
  import Pricing from './components/pricing.svelte';
  
  let isAuthenticated = false; // Set to true by default for development
  // let user = { Name: "Developer" }; // Set a default user object for development

  const handleLogin = (event) => {
    isAuthenticated = true;
    user = event.detail;
  };
</script>

<div class="app-wrapper">
  {#if isAuthenticated}
    <Navbar {isAuthenticated} />
    <Hero />
    <Pricing />
    <div class="main-content">
      <div class="grid">
        <Todo />
        <Mood />
        <Sleep />
        <Heart />
        <Step />
        <Calorie />
      </div>
    </div>
    <Footer />
  {/if}

  {#if !isAuthenticated}
    <div class="app-container">
      <div class="left-half">
        <LoginComponent on:login={handleLogin} />
      </div>
      <div class="right-half"></div>
    </div>
  {/if}
</div>

<style>
  /* Make the app-wrapper take up the full viewport height */
  .app-wrapper {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
  }

  /* main-content will expand to fill available space */
  .main-content {
    flex: 1;
    display: flex;
    justify-content: center;
    padding-bottom: 70px; /* Prevents overlap with fixed footer */
  }

  .app-container {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    color: black;
    font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
    margin-bottom: 20px;
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

  .grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr); /* 3 columns */
    grid-template-rows: repeat(2, auto); /* 2 rows */
    gap: 1rem; /* Space between items */
    justify-items: center;
    margin: 50px;
  }

  .welcome-message {
    margin-top: 2rem;
    font-size: 1.5rem;
    text-align: center;
  }
</style>
