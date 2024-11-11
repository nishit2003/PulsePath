<script>
  import { Modal, Button } from "flowbite-svelte";
  import { Radar } from 'svelte-chartjs';
  import { Chart, registerables } from 'chart.js';

  Chart.register(...registerables);

  // Generate random step data for the past 7 hours
  let stepData = Array.from({ length: 7 }, () => Math.floor(Math.random() * (500 - 100 + 1)) + 100); // Random steps between 100 and 500
  let totalSteps = stepData.reduce((sum, steps) => sum + steps, 0);
  let averageSteps = (totalSteps / stepData.length).toFixed(1);

  let showModal = false;
  let isEditing = Array(7).fill(false); // Track editing state for each hour
  let newSteps = [...stepData]; // Temporary storage for new steps during editing

  function toggleModal() {
    showModal = !showModal;
  }

  function logSteps() {
    const newStepsValue = Math.floor(Math.random() * (500 - 100 + 1)) + 100;
    stepData = [newStepsValue, ...stepData.slice(0, 6)]; // Add new value and remove oldest
    updateTotals();
  }

  function toggleEdit(index) {
    isEditing[index] = !isEditing[index];
    newSteps[index] = stepData[index];
  }

  function saveSteps(index) {
    if (newSteps[index] !== null) {
      stepData[index] = Number(newSteps[index]);
      isEditing[index] = false;
      updateTotals();
    }
  }

  function updateTotals() {
    totalSteps = stepData.reduce((sum, steps) => sum + steps, 0);
    averageSteps = (totalSteps / stepData.length).toFixed(1);
  }

  const radarOptions = {
    responsive: true,
    scales: {
      r: {
        beginAtZero: true,
        max: 500,
        ticks: { color: "#388e3c" },
        grid: { color: "#c8e6c9" },
      }
    },
    plugins: {
      legend: { display: false },
    }
  };
</script>

<div class="step-counter">
  <div class="header">
    <h2>Last 7 Hours Steps <button on:click={toggleModal} class="progress-btn">Show Progress</button></h2>
    <button on:click={logSteps} class="log-btn">Log Steps</button>
  </div>
  
  <ul class="step-list">
    {#each stepData as steps, index}
      <li>
        Hour {index + 1}:
        {#if isEditing[index]}
          <input type="number" bind:value={newSteps[index]} min="0" max="1000" class="edit-input" /> steps
          <button on:click={() => saveSteps(index)} class="save-btn">Save</button>
        {:else}
          {steps} steps
          <button on:click={() => toggleEdit(index)} class="edit-btn">Edit</button>
        {/if}
      </li>
    {/each}
  </ul>

  <p class="total-steps">Total Steps: {totalSteps}</p>
  <p class="average-steps">Average Steps: {averageSteps}</p>

  <Modal open={showModal} on:close={toggleModal} placement="center">
    <div class="progress-container">
      <h1 class="progress-title">Steps Progress Radar</h1>
      <Radar {radarOptions} data={{
        labels: Array.from({ length: 7 }, (_, i) => `Hour ${i + 1}`),
        datasets: [{
          data: stepData,
          backgroundColor: 'rgba(76, 175, 80, 0.2)',
          borderColor: '#4caf50',
          pointBackgroundColor: '#388e3c',
        }]
      }} />
      <Button color="light" class="close-btn" on:click={toggleModal}>Close</Button>
    </div>
  </Modal>
</div>

<style>
  .step-counter {
    background: #e8f5e9;
    padding: 1.5rem;
    border-radius: 30px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    text-align: center;
    width: 400px;
    margin-left: 15px;
    height: fit-content;
  }

  .header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1rem;
  }

  h2 {
    font-size: 1.5rem;
    color: #4caf50;
  }

  .log-btn, .progress-btn {
    background: #4caf50;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    padding: 0.3rem 0.7rem;
    font-size: 0.9rem;
    transition: background-color 0.3s;
  }

  .log-btn:hover, .progress-btn:hover {
    background: #388e3c;
  }

  .step-list {
    list-style-type: none;
    padding: 0;
    margin: 0;
    color: #333;
  }

  .step-list li {
    padding: 0.3rem;
    font-size: 1rem;
    background: #c8e6c9;
    margin-bottom: 0.3rem;
    border-radius: 5px;
    display: flex;
    justify-content: space-between;
  }

  .edit-btn, .save-btn {
    background: #00796b;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    padding: 0.3rem 0.5rem;
    font-size: 0.9rem;
    margin-left: 0.5rem;
  }

  .edit-btn:hover, .save-btn:hover {
    background: #004d40;
  }

  .edit-input {
    width: 5rem;
    text-align: center;
    margin-right: 0.2rem;
    border: 1px solid #ccc;
    border-radius: 3px;
    padding: 0.2rem;
  }

  .total-steps, .average-steps {
    font-size: 1.2rem;
    color: #4caf50;
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
    color: #388e3c;
    margin-bottom: 1rem;
    font-weight: bold;
  }

  .close-btn {
    font-size: 1rem;
    background-color: #4caf50;
    border-radius: 10px;
    color: white;
    margin-top: 1rem;
    transition: background-color 0.3s;
  }

  .close-btn:hover {
    background-color: #388e3c;
  }
</style>
