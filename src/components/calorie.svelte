<script>
  // @ts-ignore
  import { writable } from 'svelte/store';

  // Array to store calorie entries with timestamp
  let calorieEntries = [];
  let totalCalories = 0;

  // For managing new entry input
  let newCalorieInput = "";

  // Edit state management
  let isEditing = Array(0).fill(false); // Tracks if an entry is being edited
  let editCalorieInput = ""; // Temporary storage for edited calorie value

  // Function to log a new calorie entry
  function logCalories() {
    // @ts-ignore
    if (newCalorieInput && !isNaN(newCalorieInput)) {
      const calories = parseInt(newCalorieInput);
      const timestamp = new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
      
      calorieEntries = [...calorieEntries, { time: timestamp, calories }];
      totalCalories += calories;
      newCalorieInput = ""; // Clear the input after logging
      isEditing = Array(calorieEntries.length).fill(false); // Update edit state array length
    }
  }

  // Function to toggle edit mode for a specific entry
  function toggleEdit(index) {
    isEditing = isEditing.map((_, i) => i === index ? !isEditing[i] : false); // Only one entry can be edited at a time
    editCalorieInput = calorieEntries[index].calories; // Set the current calorie value in edit input
  }

  // Function to save the edited calorie entry
  function saveEdit(index) {
    // @ts-ignore
    if (editCalorieInput && !isNaN(editCalorieInput)) {
      const newCalories = parseInt(editCalorieInput);
      totalCalories = totalCalories - calorieEntries[index].calories + newCalories; // Update total calories
      calorieEntries[index].calories = newCalories; // Update the entry's calories
      isEditing[index] = false; // Exit editing mode
    }
  }
</script>

<div class="calorie-counter">
  <div class="header">
    <h2>Calorie Intake</h2>
  </div>

  <!-- Input and button for new calorie entry -->
  <div class="entry-input">
    <input
      type="number"
      bind:value={newCalorieInput}
      placeholder="Enter calories"
      min="0"
      class="calorie-input"
    />
    <button on:click={logCalories} class="log-btn">Log Calories</button>
  </div>

  <!-- Display each calorie entry with timestamp and edit functionality -->
  <ul class="calorie-list">
    {#each calorieEntries as entry, index}
      <li>
        {entry.time} - 
        {#if isEditing[index]}
          <input
            type="number"
            bind:value={editCalorieInput}
            min="0"
            class="edit-input"
          /> kcal
          <button on:click={() => saveEdit(index)} class="save-btn">Save</button>
        {:else}
          {entry.calories} kcal
          <button on:click={() => toggleEdit(index)} class="edit-btn">Edit</button>
        {/if}
      </li>
    {/each}
  </ul>

  <!-- Display total calorie intake for the day -->
  <p class="total-calories">Total Intake Today: {totalCalories} kcal</p>
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

  .calorie-list {
    list-style-type: none;
    padding: 0;
    margin: 0;
    color: #333;
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
</style>
