<!-- src/components/WeeklyProgress.svelte -->
<script>
  import { Modal, Button } from "flowbite-svelte";
  import { Line } from 'svelte-chartjs';
  import { Chart, registerables } from 'chart.js';
  Chart.register(...registerables);

  export let showModal = false;
  export let onClose;

  // Dummy weekly data
  let weeklyData = {
    sleep: [7, 6, 8, 5, 7.5, 8, 6.5],
    waterIntake: [8, 7, 9, 6, 8, 8, 7],
    steps: [12000, 10000, 14000, 8000, 11000, 13000, 12000],
    calories: [2000, 1800, 2200, 1900, 2100, 2000, 1950]
  };

  // Days of the week for labels
  const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];

  // Chart configurations
  const chartOptions = {
    responsive: true,
    plugins: {
      legend: { display: true }
    },
    scales: {
      x: { title: { display: true, text: 'Days of the Week' } },
      y: { title: { display: true, text: 'Value' } }
    }
  };
</script>

<Modal open={showModal} on:close={onClose} placement="center">
  <div class="weekly-progress">
    <h1 class="title">Weekly Progress</h1>
    
    <div class="chart-container">
      <h2>Sleep (Hours)</h2>
      <Line {chartOptions} data={{
        labels: days,
        datasets: [{
          label: 'Sleep',
          data: weeklyData.sleep,
          borderColor: '#4db6ac',
          fill: false,
        }]
      }} />

      <h2>Water Intake (Cups)</h2>
      <Line {chartOptions} data={{
        labels: days,
        datasets: [{
          label: 'Water Intake',
          data: weeklyData.waterIntake,
          borderColor: '#8bc34a',
          fill: false,
        }]
      }} />

      <h2>Steps</h2>
      <Line {chartOptions} data={{
        labels: days,
        datasets: [{
          label: 'Steps',
          data: weeklyData.steps,
          borderColor: '#ff9800',
          fill: false,
        }]
      }} />

      <h2>Calories (kcal)</h2>
      <Line {chartOptions} data={{
        labels: days,
        datasets: [{
          label: 'Calories',
          data: weeklyData.calories,
          borderColor: '#f44336',
          fill: false,
        }]
      }} />
    </div>

    <Button color="light" class="close-btn mt-4" on:click={onClose}>Close</Button>
  </div>
</Modal>

<style>
  .weekly-progress {
    padding: 2rem;
    background: #fef5d4;
    border-radius: 20px;
    box-shadow: 0px 5px 15px rgba(0, 0, 0, 0.1);
    text-align: center;
    max-width: 600px;
    margin: auto;
  }

  .title {
    font-size: 2rem;
    color: #6e5c41;
    margin-bottom: 1.5rem;
  }

  .chart-container {
    margin-top: 1rem;
  }

  .close-btn {
    background-color: #ffd36b;
    color: #4a4a4a;
    border-radius: 12px;
    padding: 0.5rem 1.5rem;
    margin-top: 1rem;
    font-weight: bold;
    transition: background-color 0.3s;
  }

  .close-btn:hover {
    background-color: #ffcb4d;
  }
</style>
