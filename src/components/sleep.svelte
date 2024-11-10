<!-- src/components/SleepTracker.svelte -->
<script>
  // Generate random sleep data for the past 7 days
  let sleepData = Array.from({ length: 7 }, () => Math.floor(Math.random() * (9 - 4 + 1)) + 4); // Random sleep between 4 to 9 hours
  let averageSleep = (sleepData.reduce((sum, hours) => sum + hours, 0) / sleepData.length).toFixed(1);
</script>

<div class="sleep-tracker">
  <h2>Past 7 Sleep Analysis</h2>
  
  <!-- Display sleep data for each day -->
  <ul class="sleep-list">
    {#each sleepData as hours, index}
      <li>Day {index + 1}: {hours} hours</li>
    {/each}
  </ul>

  <!-- Display average sleep duration -->
  <p class="average-sleep">Average Sleep: {averageSleep} hours</p>
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
    /* margin: 1rem auto; */
  }

  h2 {
    font-size: 1.5rem;
    color: #4a4a4a;
    margin-bottom: 1rem;
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
  }

  .average-sleep {
    font-size: 1.2rem;
    color: #00796b;
    margin-top: 1rem;
  }
</style>
