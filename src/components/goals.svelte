<!-- src/components/SetGoals.svelte -->
<script>
  import { Modal, Button } from "flowbite-svelte";
  
  export let showModal = false;
  export let onClose;

  // Goal values
  let sleepGoal = 8; // hours
  let waterGoal = 8; // cups
  let stepsGoal = 10000; // steps
  let caloriesGoal = 2000; // kcal

  function saveGoals() {
    console.log("Goals saved:", { sleepGoal, waterGoal, stepsGoal, caloriesGoal });
    onClose(); // Close the modal
  }
</script>

<Modal open={showModal} on:close={onClose} placement="center">
  <div class="goals-container">
    <h1 class="goals-title">🎯 Set Your Daily Goals</h1>

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
    padding: 2.5rem;
    background: #fff7e6;
    border-radius: 20px;
    box-shadow: 0px 10px 25px rgba(0, 0, 0, 0.15);
    text-align: center;
    max-width: 400px;
    margin: 1rem auto;
    transition: transform 0.3s ease;
  }

  .goals-title {
    font-size: 2rem;
    color: #6e5c41;
    font-weight: bold;
    margin-bottom: 1.5rem;
    display: flex;
    align-items: center;
    justify-content: center;
    animation: fadeIn 0.6s ease;
  }

  .goal-input {
    display: flex;
    flex-direction: column;
    margin-bottom: 1rem;
    text-align: left;
    padding: 0.5rem;
    background-color: #fef5d4;
    border-radius: 12px;
    box-shadow: 0px 3px 10px rgba(0, 0, 0, 0.05);
    transition: background-color 0.3s;
  }

  .goal-input:hover {
    background-color: #ffebb5;
  }

  .goal-input label {
    font-size: 1.1rem;
    color: #4a4a4a;
    margin-bottom: 0.5rem;
    font-weight: 500;
  }

  .goal-input input {
    padding: 0.6rem;
    border: 1px solid #ddd;
    border-radius: 10px;
    text-align: center;
    font-size: 1rem;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    transition: box-shadow 0.3s ease;
  }

  .goal-input input:focus {
    box-shadow: 0px 5px 15px rgba(0, 0, 0, 0.2);
  }

  .save-btn {
    font-size: 1.1rem;
    background-color: #ffd36b;
    color: #4a4a4a;
    border-radius: 15px;
    padding: 0.5rem 1.2rem;
    font-weight: bold;
    transition: background-color 0.3s, transform 0.2s;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .save-btn:hover {
    background-color: #ffcb4d;
    transform: scale(1.05);
  }

  @keyframes fadeIn {
    0% { opacity: 0; }
    100% { opacity: 1; }
  }
</style>
