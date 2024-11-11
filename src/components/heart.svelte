<script>
  // Generate random heartbeat data for the past 7 hours
  let heartbeatData = Array.from({ length: 7 }, () => Math.floor(Math.random() * (100 - 60 + 1)) + 60); // Random bpm between 60 and 100
  let averageHeartbeat = (heartbeatData.reduce((sum, bpm) => sum + bpm, 0) / heartbeatData.length).toFixed(1);
</script>

<div class="heartbeat-tracker">
  <h2>Last 7 Hours Heartbeat</h2>
  
  <!-- Display heartbeat data for each hour -->
  <ul class="heartbeat-list">
    {#each heartbeatData as bpm, index}
      <li>Hour {index + 1}: {bpm} bpm</li>
    {/each}
  </ul>

  <!-- Display average heartbeat -->
  <p class="average-heartbeat">Average Heartbeat: {averageHeartbeat} bpm</p>
</div>

<style>
  .heartbeat-tracker {
    background: #fdf6f6;
    padding: 1.5rem;
    border-radius: 30px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    text-align: center;
    width: 400px;
    margin-left: 15px;
  }

  h2 {
    font-size: 1.5rem;
    color: #d9534f;
    margin-bottom: 1rem;
  }

  .heartbeat-list {
    list-style-type: none;
    padding: 0;
    margin: 0;
    color: #333;
  }

  .heartbeat-list li {
    padding: 0.3rem;
    font-size: 1rem;
    background: #fdecea;
    margin-bottom: 0.3rem;
    border-radius: 5px;
  }

  .average-heartbeat {
    font-size: 1.2rem;
    color: #d9534f;
    margin-top: 1rem;
  }
</style>
