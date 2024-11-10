<!-- src/components/UserInfo.svelte -->
<script>
  import { Modal, Button } from "flowbite-svelte"; // Import Modal from Flowbite
  
  export let user = { name: "Nishit Grover", username: "nishit123" }; // Default user info
  export let showModal = false; // Control modal visibility
  export let onClose; // Function to close the modal

  // Mock health stats
  const healthStats = {
    waterIntake: "8 cups",
    sleepHours: "7 hours",
    exercise: "30 mins",
  };

  // Health tracking tips
  const tips = [
    "Stay hydrated! Aim for at least 8 cups of water each day.",
    "Aim for 7-8 hours of quality sleep every night.",
    "Keep active! Try to exercise for 30 minutes daily.",
    "Remember to log your meals and daily mood to track progress.",
  ];
</script>

<Modal open={showModal} on:close={onClose} placement="center">
  <div class="modal-content">
    <h1 class="info-title">User Information</h1>
    <div class="info-box">
      <p><strong>Name:</strong> {user.name}</p>
      <p><strong>Username:</strong> {user.username}</p>
    </div>

    <h1 class="info-title">Today's Health Stats</h1>
    <div class="info-box">
      <p><strong>Water Intake:</strong> {healthStats.waterIntake}</p>
      <p><strong>Sleep:</strong> {healthStats.sleepHours}</p>
      <p><strong>Exercise:</strong> {healthStats.exercise}</p>
    </div>

    <h1 class="info-title">Health Tips</h1>
    <ul class="tips-list">
      {#each tips as tip}
        <li class="tip-item">{tip}</li>
      {/each}
    </ul>

    <Button color="light" class="mt-4" on:click={onClose}>Close</Button>
  </div>
</Modal>

<style>
  .modal-content {
    padding: 2rem;
    text-align: center;
    background: #f8f9fa;
    border-radius: 20px;
  }

  .info-title {
    font-size: 1.8rem;
    color: #333;
    font-weight: bold;
    margin-bottom: 1rem;
  }

  .info-box {
    background: #f0f0f0;
    color: #333;
    padding: 1rem;
    border-radius: 15px;
    margin-bottom: 1.5rem;
  }

  .tips-list {
    list-style-type: none;
    color: #333;
    padding: 0;
    margin: 0;
  }

  .tip-item {
    font-size: 1rem;
    margin-bottom: 0.7rem;
    padding: 0.7rem;
    background: #e7f3ff;
    border-radius: 10px;
    transition: transform 0.3s;
  }

  .tip-item:hover {
    transform: translateY(-3px);
  }
</style>
