<!-- src/components/Navbar.svelte -->
<script>
  // @ts-ignore
  import UserInfo from './UserInfo.svelte'; // Import the UserInfo component
  import Tips from './tips.svelte';
  import Goals from './goals.svelte';
  import Date from './date.svelte';

  export let isAuthenticated = false;
  let showUserInfo = false; // State to control the UserInfo modal visibility
  let showTips = false;
  let showGoals = false; // State to control the Tips modal visibility
  let showDate = false;

  const toggleUserInfo = () => {
    showUserInfo = !showUserInfo;
  };

  const toggleTips = () => {
    showTips = !showTips;
  };

  const toggleGoals = () => {
    showGoals = !showGoals;
  };

  const toggleDate = () => {
    showDate = !showDate;
  };
</script>

<nav class="navbar">
  <div class="brand">PulsePath</div>
  <div class="links">
    <!-- svelte-ignore a11y-invalid-attribute -->
    <a href="#" on:click|preventDefault={toggleUserInfo}>User Info</a> <!-- Toggle modal on click -->
    <a href="/dashboard" on:click|preventDefault={toggleDate}>Change Date</a>
    <a href="/dashboard" on:click|preventDefault={toggleTips}>Tips</a>
    <a href="/dashboard" on:click|preventDefault={toggleGoals}>Goals</a>
    <a href="/dashboard">Info</a>
    <a href="/logout">Logout</a>
  </div>
</nav>

<!-- Render UserInfo component when showUserInfo is true -->
{#if showUserInfo}
  <UserInfo showModal={showUserInfo} onClose={toggleUserInfo} />
{/if}

<!-- Render Tips component when showTips is true -->
{#if showTips}
  <Tips showModal={showTips} onClose={toggleTips} />
{/if}
<!-- Render Goals component when showGoals is true -->
{#if showGoals}
  <Goals showModal={showGoals} onClose={toggleGoals} />
{/if}

<!-- Render Date component when showDate is true -->
{#if showDate}
  <Date showModal={showDate} onClose={toggleDate} />
{/if}

<style>
  .navbar {
    display: flex;
    justify-content: space-between;
    padding: 1rem;
    background-color: #f5ebe2;
    color: white;
    font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  }

  .brand {
    font-size: 1.5rem;
    font-weight: bold;
    color: #927458;
  }

  .links a {
    margin-left: 1rem;
    color: #927458;
    text-decoration: none;
  }

  .links a:hover {
    text-decoration: underline;
  }
</style>
