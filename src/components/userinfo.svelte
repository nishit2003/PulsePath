<script>
  import { Modal, Button } from "flowbite-svelte"; // Import Modal from Flowbite
  
  export let user = {
    name: "Nishit Grover",
    username: "nishit123",
    email: "nishit@example.com",
    age: 22,
    height: 175, // in cm
    weight: 70,  // in kg
  };
  export let showModal = false;
  export let onClose;

  // Calculate BMI based on height and weight
  let bmi = (user.weight / ((user.height / 100) ** 2)).toFixed(1);

  // Editing state
  let isEditing = false;
  let editedHeight = user.height;
  let editedWeight = user.weight;

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

  // Toggle edit mode
  function toggleEdit() {
    isEditing = !isEditing;
    editedHeight = user.height;
    editedWeight = user.weight;
  }

  // Save edited height and weight, and recalculate BMI
  function saveUserInfo() {
    user.height = editedHeight;
    user.weight = editedWeight;
    bmi = (user.weight / ((user.height / 100) ** 2)).toFixed(1); // Recalculate BMI
    isEditing = false;
  }
</script>

<Modal open={showModal} on:close={onClose} placement="center">
  <div class="modal-content">
    <h1 class="info-title">User Profile</h1>
    
    <!-- User Basic Info -->
    <div class="info-section">
      <h2>User Details</h2>
      <p><strong>Name:</strong> {user.name}</p>
      <p><strong>Age:</strong> {user.age}</p>
      <p><strong>Username:</strong> {user.username}</p>
      <p><strong>Email:</strong> {user.email}</p>
      
    </div>

    <!-- Editable Health Info -->
    <div class="info-section">
      <h2>Health Info</h2>
      {#if isEditing}
        <div class="edit-section">
          <label>Height (cm):</label>
          <input type="number" bind:value={editedHeight} min="50" max="250" class="input-field" />

          <label>Weight (kg):</label>
          <input type="number" bind:value={editedWeight} min="20" max="300" class="input-field" />
          <button on:click={saveUserInfo} class="save-btn">Save</button>
        </div>
      {:else}
        <p><strong>Height:</strong> {user.height} cm</p>
        <p><strong>Weight:</strong> {user.weight} kg</p>
        <p><strong>BMI:</strong> {bmi}</p>
        <button on:click={toggleEdit} class="edit-btn">Edit</button>
      {/if}
    </div>


    <!-- Health Tips -->
    <div class="info-section">
      <h2>Health Tips</h2>
      <ul class="tips-list">
        {#each tips as tip}
          <li class="tip-item">{tip}</li>
        {/each}
      </ul>
    </div>

    <!-- Close Button -->
    <Button color="light" class="mt-4 close-btn" on:click={onClose}>Close</Button>
  </div>
</Modal>

<style>
  .modal-content {
    padding: 2rem;
    text-align: center;
    background: #ffffff;
    border-radius: 20px;
    box-shadow: 0px 5px 15px rgba(0, 0, 0, 0.2);
  }

  .info-title {
    font-size: 2rem;
    color: #3a3a3a;
    font-weight: bold;
    margin-bottom: 1.5rem;
  }

  .info-section {
    background: #f9f9f9;
    border-radius: 15px;
    padding: 1rem;
    margin-bottom: 1.5rem;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.05);
  }

  h2 {
    font-size: 1.4rem;
    color: #5a5a5a;
    margin-bottom: 1rem;
  }

  .edit-btn, .save-btn {
    background: #007bff;
    color: white;
    border: none;
    border-radius: 10px;
    cursor: pointer;
    padding: 0.4rem 0.8rem;
    font-size: 0.9rem;
    margin-top: 1rem;
    transition: background 0.3s;
  }

  .edit-btn:hover, .save-btn:hover {
    background: #0056b3;
  }

  .input-field {
    width: 80px;
    padding: 0.4rem;
    margin-top: 0.5rem;
    margin-bottom: 1rem;
    border: 1px solid #ddd;
    border-radius: 8px;
    text-align: center;
    font-size: 1rem;
  }

  .tips-list {
    list-style-type: none;
    padding: 0;
    margin: 0;
    color: #3a3a3a;
  }

  .tip-item {
    background: #e8f5e9;
    border-radius: 8px;
    padding: 0.6rem;
    margin-bottom: 0.5rem;
    transition: transform 0.3s;
    color: #3a3a3a;
    font-size: 0.95rem;
  }

  .tip-item:hover {
    transform: translateY(-3px);
  }

  .close-btn {
    font-size: 1rem;
    background-color: #007bff;
    border-radius: 10px;
    color: white;
    transition: background 0.3s;
  }

  .close-btn:hover {
    background-color: #0056b3;
  }
</style>
