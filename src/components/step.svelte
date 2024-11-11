<script>
  // Generate random step data for the past 7 hours
  let stepData = Array.from({ length: 7 }, () => Math.floor(Math.random() * (500 - 100 + 1)) + 100); // Random steps between 100 and 500
  let totalSteps = stepData.reduce((sum, steps) => sum + steps, 0);
  let averageSteps = (totalSteps / stepData.length).toFixed(1);

  // Function to log new steps
  function logSteps() {
    const newSteps = Math.floor(Math.random() * (500 - 100 + 1)) + 100; // Random steps between 100 and 500
    stepData = [newSteps, ...stepData.slice(0, 6)]; // Add new value and remove oldest
    totalSteps = stepData.reduce((sum, steps) => sum + steps, 0); // Update total
    averageSteps = (totalSteps / stepData.length).toFixed(1); // Recalculate average
  }
</script>

<div class="step-counter">
  <div class="header">
    <h2>Last 7 Hours Steps</h2>
    <button on:click={logSteps} class="log-btn">Log Steps</button>
  </div>
  
  <!-- Display step data for each hour -->
  <ul class="step-list">
    {#each stepData as steps, index}
      <li>Hour {index + 1}: {steps} steps</li>
    {/each}
  </ul>

  <!-- Display total and average steps -->
  <p class="total-steps">Total Steps: {totalSteps}</p>
  <p class="average-steps">Average Steps: {averageSteps}</p>
</div>

<style>
  .step-counter {
    background: #f3f9f3;
    padding: 1.5rem;
    border-radius: 30px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    text-align: center;
    width: 400px;
    margin-left: 15px;
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

  .log-btn {
    background: #4caf50;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    padding: 0.3rem 0.7rem;
    font-size: 0.9rem;
  }

  .log-btn:hover {
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
    background: #e8f5e9;
    margin-bottom: 0.3rem;
    border-radius: 5px;
  }

  .total-steps, .average-steps {
    font-size: 1.2rem;
    color: #4caf50;
    margin-top: 0.5rem;
  }
</style>
