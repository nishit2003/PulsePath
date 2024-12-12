<script>
  import { Modal, Button } from "flowbite-svelte";
  import { Bar } from 'svelte-chartjs';
  import { Chart, registerables } from 'chart.js';

  Chart.register(...registerables);

  // Generate random sleep data for the past 7 days
  let sleepData = Array.from({ length: 7 }, () => Math.floor(Math.random() * (9 - 4 + 1)) + 4); // Random sleep between 4 to 9 hours
  let averageSleep = (sleepData.reduce((sum, hours) => sum + hours, 0) / sleepData.length).toFixed(1);

  let isEditing = Array(7).fill(false); // Track editing state for each day
  let newHours = Array(7).fill(null); // Temporary storage for new hours during editing
  let showModal = false; // Track modal visibility for graph

  function toggleModal() {
    showModal = !showModal;
  }

  function toggleEdit(index) {
    isEditing[index] = !isEditing[index];
    newHours[index] = sleepData[index]; // Set the current hours as the default value
  }

  function saveHours(index) {
    if (newHours[index] !== null) {
      sleepData[index] = Number(newHours[index]);
      averageSleep = (sleepData.reduce((sum, hours) => sum + hours, 0) / sleepData.length).toFixed(1);
      isEditing[index] = false;
    }
  }

  const barOptions = {
    responsive: true,
    plugins: {
      legend: { display: false }
    },
    scales: {
      x: { title: { display: true, text: 'Day' } },
      y: { title: { display: true, text: 'Hours' } }
    }
  };
</script>

<div class="sleep-tracker">
  <h2>Past 7 Days Sleep Analysis <button class="progress-button" on:click={toggleModal}>Show Progress</button></h2>

  <!-- Display sleep data for each day with edit functionality -->
  <ul class="sleep-list">
    {#each sleepData as hours, index}
      <li>
        Day {index + 1}:
        {#if isEditing[index]}
          <input type="number" bind:value={newHours[index]} min="0" max="24" class="edit-input" /> hours
          <button on:click={() => saveHours(index)} class="save-btn">Save</button>
        {:else}
          {hours} hours
          <button on:click={() => toggleEdit(index)} class="edit-btn">Edit</button>
        {/if}
      </li>
    {/each}
  </ul>

  <!-- Display average sleep duration -->
  <p class="average-sleep">Average Sleep: {averageSleep} hours</p>

  <!-- Sleep Progress Modal -->
  <Modal open={showModal} placement="center">
    <div class="progress-container">
      <h1 class="progress-title">Sleep Progress Over the Last 7 Days</h1>
      
      <!-- Bar Chart for Sleep Data -->
      <Bar {barOptions} data={{
        labels: Array.from({ length: 7 }, (_, i) => `Day ${i + 1}`),
        datasets: [{
          label: 'Hours Slept',
          data: sleepData,
          backgroundColor: '#4db6ac',
        }]
      }} />

      <Button color="light" class="close-btn" on:click={toggleModal}>Close</Button>
    </div>
  </Modal>
</div>

<style>
  .sleep-tracker {
    background: #f9f9f9;
    padding: 1.5rem;
    border-radius: 30px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    text-align: center;
    width: 400px;
    margin-left: 15px;
    height: fit-content;
  }

  h2 {
    font-size: 1.5rem;
    color: #4a4a4a;
    margin-bottom: 1rem;
  }

  .progress-button {
    background: #4db6ac;
    color: white;
    border: none;
    border-radius: 5px;
    padding: 0.3rem 0.6rem;
    cursor: pointer;
    font-size: 0.9rem;
    margin-left: 0.5rem;
    transition: background-color 0.3s;
  }

  .progress-button:hover {
    background: #00796b;
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
    color: #00796b;
    margin-bottom: 1rem;
    font-weight: bold;
  }

  .close-btn {
    font-size: 1rem;
    background-color: #4db6ac;
    border-radius: 10px;
    color: white;
    margin-top: 1rem;
    transition: background-color 0.3s;
  }

  .close-btn:hover {
    background-color: #00796b;
  }

  .sleep-list {
    list-style-type: none;
    padding: 0;
    margin: 0;
    color: #333;
  }

  .sleep-list li {
    padding: 0.3rem;
    font-size: 1rem;
    background: #e3f2fd;
    margin-bottom: 0.3rem;
    border-radius: 5px;
    display: flex;
    align-items: center;
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
    width: 3rem;
    text-align: center;
    margin-right: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 3px;
    padding: 0.2rem;
  }

  .average-sleep {
    font-size: 1.2rem;
    color: #00796b;
    margin-top: 1rem;
  }
</style>
