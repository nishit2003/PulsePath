<!-- src/components/Navbar.svelte -->
<script>
  import UserInfo from './UserInfo.svelte'; // Import the UserInfo component

  export let isAuthenticated = false;
  let showUserInfo = false; // State to control the UserInfo modal visibility

  const toggleUserInfo = () => {
    showUserInfo = !showUserInfo;
  };
</script>

<nav class="navbar">
  <div class="brand">PulsePath</div>
  <div class="links">
    <!-- svelte-ignore a11y-invalid-attribute -->
    <a href="#" on:click|preventDefault={toggleUserInfo}>User Info</a> <!-- Toggle modal on click -->
    <a href="/dashboard">Change Date</a>
    <a href="/dashboard">Info</a>
    <a href="/logout">Logout</a>
  </div>
</nav>

<!-- Render UserInfo component when showUserInfo is true -->
{#if showUserInfo}
  <UserInfo showModal={showUserInfo} onClose={toggleUserInfo} />
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
