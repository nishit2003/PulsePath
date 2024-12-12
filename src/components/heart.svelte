<script>
  import { Modal, Button } from "flowbite-svelte";
  import { Line } from 'svelte-chartjs';
  import { Chart, registerables } from 'chart.js';

  Chart.register(...registerables);

  // Generate random water intake data for the past 7 hours (between 0.5 and 1.5 cups per hour)
  let waterIntakeData = Array.from({ length: 7 }, () => (Math.random() * (1.5 - 0.5) + 0.5).toFixed(1));
  let totalWaterIntake = waterIntakeData.reduce((sum, cups) => sum + parseFloat(cups), 0).toFixed(1);
  let targetGoal = 8; // Target goal in cups

  let isEditing = Array(7).fill(false); // Track editing state for each hour
  let newCups = Array(7).fill(null); // Temporary storage for new cups during editing
  let showModal = false;

  function toggleModal() {
    showModal = !showModal;
  }

  function toggleEdit(index) {
    isEditing[index] = !isEditing[index];
    newCups[index] = waterIntakeData[index]; // Set the current cups as the default value
  }

  function saveCups(index) {
    if (newCups[index] !== null) {
      waterIntakeData[index] = Number(newCups[index]).toFixed(1);
      totalWaterIntake = waterIntakeData.reduce((sum, cups) => sum + parseFloat(cups), 0).toFixed(1);
      isEditing[index] = false;
    }
  }

  const lineOptions = {
    responsive: true,
    plugins: {
      legend: { display: false }
    },
    scales: {
      x: { title: { display: true, text: 'Hour' } },
      y: { title: { display: true, text: 'Cups' }, beginAtZero: true, max: 2 },
    }
  };
</script>

<div class="water-tracker">
  <h2>Last 7 Hours Water Intake <button class="progress-button" on:click={toggleModal}>Show Progress</button></h2>

  <!-- Display water intake data for each hour with edit functionality -->
  <ul class="water-list">
    {#each waterIntakeData as cups, index}
      <li>
        Hour {index + 1}:
        {#if isEditing[index]}
          <input type="number" bind:value={newCups[index]} min="0" max="2" step="0.1" class="edit-input" /> cups
          <button on:click={() => saveCups(index)} class="save-btn">Save</button>
        {:else}
          {cups} cups
          <button on:click={() => toggleEdit(index)} class="edit-btn">Edit</button>
        {/if}
      </li>
    {/each}
  </ul>

  <!-- Display total water intake and target goal -->
  <p class="total-water-intake">Total Water Intake: {totalWaterIntake} cups / {targetGoal} cups</p>

  <!-- Water Intake Progress Modal -->
  <Modal open={showModal} placement="center">
    <div class="progress-container">
      <h1 class="progress-title">Water Intake Progress</h1>
      
      <!-- Line Chart for Water Intake Data -->
      <Line {lineOptions} data={{
        labels: Array.from({ length: 7 }, (_, i) => `Hour ${i + 1}`),
        datasets: [{
          label: 'Water Intake',
          data: waterIntakeData,
          borderColor: '#ffbf47',
          backgroundColor: '#ffedd5',
          fill: true,
          tension: 0.4, // Curved line
        }]
      }} />

      <Button color="light" class="close-btn" on:click={toggleModal}>Close</Button>
    </div>
  </Modal>
</div>

<style>
  .water-tracker {
    background: #fdf2e9;
    padding: 1.5rem;
    border-radius: 30px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    text-align: center;
    width: 400px;
    margin-left: 15px;
    /* height: fit-content; */
  }

  h2 {
    font-size: 1.5rem;
    color: #b36b00;
    margin-bottom: 1rem;
  }

  .progress-button {
    background: #ffbf47;
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
    background: #b36b00;
  }

  .progress-container {
    padding: 2rem;
    background: #fffaf3;
    border-radius: 20px;
    box-shadow: 0px 10px 25px rgba(0, 0, 0, 0.15);
    text-align: center;
    max-width: 500px;
    margin: auto;
  }

  .progress-title {
    font-size: 1.8rem;
    color: #b36b00;
    margin-bottom: 1rem;
    font-weight: bold;
  }

  .close-btn {
    font-size: 1rem;
    background-color: #ffbf47;
    border-radius: 10px;
    color: white;
    margin-top: 1rem;
    transition: background-color 0.3s;
  }

  .close-btn:hover {
    background-color: #b36b00;
  }

  .water-list {
    list-style-type: none;
    padding: 0;
    margin: 0;
    color: #333;
  }

  .water-list li {
    padding: 0.3rem;
    font-size: 1rem;
    background: #ffedd5;
    margin-bottom: 0.3rem;
    border-radius: 5px;
  }

  .total-water-intake {
    font-size: 1.2rem;
    color: #b36b00;
    margin-top: 1rem;
  }
</style>
