<!-- src/components/UserInfo.svelte -->
<script>
  import { Modal, Button } from "flowbite-svelte";

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

  function toggleEdit() {
    isEditing = !isEditing;
    editedHeight = user.height;
    editedWeight = user.weight;
  }

  function saveUserInfo() {
    user.height = editedHeight;
    user.weight = editedWeight;
    bmi = (user.weight / ((user.height / 100) ** 2)).toFixed(1);
    isEditing = false;
    alert("User info saved successfully!");
  }
</script>

<Modal open={showModal} on:close={onClose} placement="center">
  <div class="modal-content">
    <h1 class="info-title">👤 User Profile</h1>

    <div class="info-section">
      <h2>User Details</h2>
      <p><strong>Name:</strong> {user.name}</p>
      <p><strong>Age:</strong> {user.age}</p>
      <p><strong>Username:</strong> {user.username}</p>
      <p><strong>Email:</strong> {user.email}</p>
    </div>

    <div class="info-section">
      <h2>Health Info</h2>
      {#if isEditing}
        <div class="edit-section">
          <label>Height (cm):</label>
          <input type="number" bind:value={editedHeight} min="50" max="250" class="input-field" />
          <br>
          <label>Weight (kg):</label>
          <input type="number" bind:value={editedWeight} min="20" max="300" class="input-field" />
          <br>
          <button on:click={saveUserInfo} class="save-btn">Save</button>
        </div>
      {:else}
        <p><strong>Height:</strong> {user.height} cm</p>
        <p><strong>Weight:</strong> {user.weight} kg</p>
        <p><strong>BMI:</strong> {bmi}</p>
        <button on:click={toggleEdit} class="edit-btn">Edit</button>
      {/if}
    </div>

    <Button color="light" class="close-btn" on:click={onClose}>Close</Button>
  </div>
</Modal>

<style>
  .modal-content {
    padding: 2.5rem;
    background: #fef5d4;
    border-radius: 20px;
    box-shadow: 0px 10px 25px rgba(0, 0, 0, 0.15);
    text-align: center;
    max-width: 500px;
    margin: 1rem auto;
    transition: transform 0.3s ease;
  }

  .info-title {
    font-size: 2rem;
    color: #6e5c41;
    font-weight: bold;
    margin-bottom: 1.5rem;
    display: flex;
    align-items: center;
    justify-content: center;
    animation: fadeIn 0.6s ease;
  }

  .info-section {
    background: #fff7e6;
    border-radius: 15px;
    padding: 1.5rem;
    margin-bottom: 1.5rem;
    box-shadow: 0px 5px 15px rgba(0, 0, 0, 0.05);
    transition: background-color 0.3s;
  }

  .info-section:hover {
    background-color: #ffebb5;
  }

  h2 {
    font-size: 1.5rem;
    color: #4a4a4a;
    margin-bottom: 1rem;
  }

  .edit-btn, .save-btn {
    background: #ffd36b;
    color: #4a4a4a;
    border: none;
    border-radius: 12px;
    cursor: pointer;
    padding: 0.5rem 1rem;
    font-size: 1rem;
    margin-top: 1rem;
    transition: background-color 0.3s, transform 0.2s;
  }

  .edit-btn:hover, .save-btn:hover {
    background-color: #ffcb4d;
    transform: scale(1.05);
  }

  .input-field {
    width: 100px;
    padding: 0.5rem;
    margin-top: 0.5rem;
    margin-bottom: 1rem;
    border: 1px solid #ddd;
    border-radius: 10px;
    text-align: center;
    font-size: 1rem;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  }

  .close-btn {
    font-size: 1rem;
    background-color: #ffd36b;
    border-radius: 12px;
    color: #4a4a4a;
    padding: 0.5rem 1.5rem;
    margin-top: 1rem;
    font-weight: bold;
    transition: background-color 0.3s, transform 0.2s;
  }

  .close-btn:hover {
    background-color: #ffcb4d;
    transform: scale(1.05);
  }

  @keyframes fadeIn {
    0% { opacity: 0; }
    100% { opacity: 1; }
  }
</style>
