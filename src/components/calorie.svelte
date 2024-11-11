<script>
  import { Modal, Button } from "flowbite-svelte";
  import { Line } from 'svelte-chartjs';
  import { Chart, registerables } from 'chart.js';

  Chart.register(...registerables);

  // Array to store calorie entries with timestamp
  let calorieEntries = [];
  let totalCalories = 0;
  let newCalorieInput = ""; // For new entry input
  let isEditing = []; // Tracks edit state for each entry
  let editCalorieInput = ""; // Temporary storage for edited calorie value
  let showModal = false; // Track modal visibility for chart
  let dailyGoal = 2000; // Dummy calorie goal

  function toggleModal() {
    showModal = !showModal;
  }

  function logCalories() {
    if (newCalorieInput && !isNaN(newCalorieInput)) {
      const calories = parseInt(newCalorieInput);
      const timestamp = new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
      calorieEntries = [...calorieEntries, { time: timestamp, calories }];
      totalCalories += calories;
      newCalorieInput = "";
      isEditing = Array(calorieEntries.length).fill(false);
    }
  }

  function toggleEdit(index) {
    isEditing = isEditing.map((_, i) => i === index ? !isEditing[i] : false);
    editCalorieInput = calorieEntries[index].calories;
  }

  function saveEdit(index) {
    if (editCalorieInput && !isNaN(editCalorieInput)) {
      const newCalories = parseInt(editCalorieInput);
      totalCalories = totalCalories - calorieEntries[index].calories + newCalories;
      calorieEntries[index].calories = newCalories;
      isEditing[index] = false;
    }
  }

  const lineOptions = {
    responsive: true,
    plugins: {
      legend: { display: false },
      tooltip: {
        callbacks: {
          label: (context) => `${context.raw} kcal`,
        },
      },
    },
    scales: {
      y: {
        beginAtZero: true,
        max: dailyGoal,
        title: { display: true, text: 'Calories' },
      },
      x: { title: { display: true, text: 'Time' } },
    },
  };
</script>

<div class="calorie-counter">
  <div class="header">
    <h2>Calorie Intake <button on:click={toggleModal} class="progress-btn">Show Progress</button></h2>
  </div>

  <div class="entry-input">
    <input type="number" bind:value={newCalorieInput} placeholder="Enter calories" min="0" class="calorie-input" />
    <button on:click={logCalories} class="log-btn">Log Calories</button>
  </div>

  <ul class="calorie-list">
    {#each calorieEntries as entry, index}
      <li>
        {entry.time} - 
        {#if isEditing[index]}
          <input type="number" bind:value={editCalorieInput} min="0" class="edit-input" /> kcal
          <button on:click={() => saveEdit(index)} class="save-btn">Save</button>
        {:else}
          {entry.calories} kcal
          <button on:click={() => toggleEdit(index)} class="edit-btn">Edit</button>
        {/if}
      </li>
    {/each}
  </ul>

  <p class="total-calories">Total Intake Today: {totalCalories} kcal</p>

  <!-- Progress Modal -->
  <Modal open={showModal} on:close={toggleModal} placement="center">
    <div class="progress-container">
      <h1 class="progress-title">Calorie Intake Progress</h1>

      <!-- Line Chart for Calorie Data -->
      <Line {lineOptions} data={{
        labels: calorieEntries.map(entry => entry.time),
        datasets: [{
          data: calorieEntries.map(entry => entry.calories),
          label: "Calories",
          borderColor: "#ff8c00",
          backgroundColor: "rgba(255, 140, 0, 0.2)",
          fill: true,
          tension: 0.4,
        }]
      }} />

      <Button color="light" class="close-btn" on:click={toggleModal}>Close</Button>
    </div>
  </Modal>
</div>

<style>
  .calorie-counter {
    background: #fff8e1;
    padding: 1.5rem;
    border-radius: 30px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    text-align: center;
    width: 400px;
    margin-left: 15px;
    color: #ff8c00;
  }

  .header {
    margin-bottom: 1rem;
  }

  h2 {
    font-size: 1.5rem;
    color: #ff8c00;
  }

  .progress-btn {
    background: #ff8c00;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    padding: 0.3rem 0.6rem;
    font-size: 0.9rem;
    margin-left: 0.5rem;
    transition: background-color 0.3s;
  }

  .progress-btn:hover {
    background: #e67e00;
  }

  .entry-input {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-bottom: 1rem;
  }

  .calorie-input {
    width: 100px;
    padding: 0.3rem;
    margin-right: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 5px;
  }

  .log-btn {
    background: #ff8c00;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    padding: 0.3rem 0.7rem;
    font-size: 0.9rem;
  }

  .log-btn:hover {
    background: #e67e00;
  }

  .calorie-list li {
    padding: 0.3rem;
    font-size: 1rem;
    background: #fff3e0;
    margin-bottom: 0.3rem;
    border-radius: 5px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .edit-btn, .save-btn {
    background: #ff8c00;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    padding: 0.3rem 0.7rem;
    font-size: 0.9rem;
    margin-left: 0.5rem;
  }

  .edit-btn:hover, .save-btn:hover {
    background: #e67e00;
  }

  .edit-input {
    width: 60px;
    padding: 0.2rem;
    margin-right: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 5px;
  }

  .total-calories {
    font-size: 1.2rem;
    color: #ff8c00;
    margin-top: 0.5rem;
  }

  .progress-container {
    padding: 2rem;
    background: #ffffff;
    border-radius: 20px;
    box-shadow: 0px 10px 25px rgba(0, 0, 0, 0.15);
    text-align: center;
    max-width: 500px;
    margin: auto;
  }

  .progress-title {
    font-size: 1.8rem;
    color: #ff8c00;
    margin-bottom: 1rem;
    font-weight: bold;
  }

  .close-btn {
    font-size: 1rem;
    background-color: #ff8c00;
    border-radius: 10px;
    color: white;
    margin-top: 1rem;
    transition: background-color 0.3s;
  }

  .close-btn:hover {
    background-color: #e67e00;
  }
</style>
