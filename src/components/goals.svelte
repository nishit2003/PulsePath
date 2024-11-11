<!-- src/components/SetGoals.svelte -->
<script>
  import { Modal, Button } from "flowbite-svelte"; // Import Modal from Flowbite
  
  export let showModal = false;
  export let onClose;

  // Goal values
  let sleepGoal = 8; // hours
  let waterGoal = 8; // cups
  let stepsGoal = 10000; // steps
  let caloriesGoal = 2000; // kcal

  function saveGoals() {
    // Here you can add functionality to save the goals, e.g., to local storage or an API
    console.log("Goals saved:", { sleepGoal, waterGoal, stepsGoal, caloriesGoal });
    onClose(); // Close the modal
  }
</script>

<Modal open={showModal} on:close={onClose} placement="center">
  <div class="goals-container">
    <h1 class="goals-title">Set Your Daily Goals</h1>

    <div class="goal-input">
      <label>Sleep (hours):</label>
      <input type="number" bind:value={sleepGoal} min="1" max="12" />
    </div>

    <div class="goal-input">
      <label>Water (cups):</label>
      <input type="number" bind:value={waterGoal} min="1" max="20" />
    </div>

    <div class="goal-input">
      <label>Steps:</label>
      <input type="number" bind:value={stepsGoal} min="1000" max="50000" step="500" />
    </div>

    <div class="goal-input">
      <label>Calories (kcal):</label>
      <input type="number" bind:value={caloriesGoal} min="500" max="5000" step="100" />
    </div>

    <Button color="light" class="save-btn mt-4" on:click={saveGoals}>Save Goals</Button>
  </div>
</Modal>

<style>
  .goals-container {
    padding: 2rem;
    background: #ffffff;
    border-radius: 20px;
    box-shadow: 0px 5px 15px rgba(0, 0, 0, 0.1);
    text-align: center;
    max-width: 400px;
    margin: 1rem auto;
  }

  .goals-title {
    font-size: 1.8rem;
    color: #4a4a4a;
    font-weight: bold;
    margin-bottom: 1.5rem;
  }

  .goal-input {
    display: flex;
    flex-direction: column;
    margin-bottom: 1rem;
    text-align: left;
  }

  .goal-input label {
    font-size: 1rem;
    color: #555;
    margin-bottom: 0.5rem;
  }

  .goal-input input {
    padding: 0.5rem;
    border: 1px solid #ddd;
    border-radius: 8px;
    text-align: center;
    font-size: 1rem;
  }

  .save-btn {
    font-size: 1rem;
    background-color: #007bff;
    color: white;
    border-radius: 10px;
    transition: background 0.3s;
  }

  .save-btn:hover {
    background-color: #0056b3;
  }
</style>
