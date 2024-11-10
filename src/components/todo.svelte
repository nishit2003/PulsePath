<!-- src/components/MedicationChecklist.svelte -->
<script>
  let newMedication = "";
  let medications = [
    { name: "Vitamin D", taken: false },
    { name: "Omega-3 Fish Oil", taken: false },
    { name: "Multivitamin", taken: false },
    { name: "Probiotic", taken: false }
  ];

  // Add a new medication to the list
  function addMedication() {
    if (newMedication.trim() !== "") {
      medications = [...medications, { name: newMedication, taken: false }];
      newMedication = ""; // Clear input
    }
  }

  // Toggle the taken status of a medication
  function toggleTaken(index) {
    medications[index].taken = !medications[index].taken;
  }

  // Remove a medication from the list
  function removeMedication(index) {
    medications = medications.filter((_, i) => i !== index);
  }
</script>

<div class="medication-container">
  <h2>Medication Checklist</h2>
  
  <!-- Input for adding new medications -->
  <div class="medication-input">
    <input
      type="text"
      placeholder="Add new medication or supplement..."
      bind:value={newMedication}
      on:keypress={(e) => e.key === 'Enter' && addMedication()}
    />
    <button on:click={addMedication}>Add</button>
  </div>

  <!-- List of medications -->
  <ul class="medication-list">
    {#each medications as { name, taken }, index}
      <li class:completed={taken}>
        <input
          type="checkbox"
          checked={taken}
          on:change={() => toggleTaken(index)}
        />
        <span>{name}</span>
        <button on:click={() => removeMedication(index)} class="delete-btn">✕</button>
      </li>
    {/each}
  </ul>
</div>

<style>
  .medication-container {
   margin-top: 10px;
   margin-left: 15px;
   background: #f7f7f7;
    padding: 1.5rem;
    border-radius: 30px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    margin-bottom: 2rem;
    width: 400px;
    color: #edbc7b;
  }

  h2 {
    font-size: 1.5rem;
    color: #caa17b;
    margin-bottom: 1rem;
  }

  .medication-input {
    display: flex;
    margin-bottom: 1rem;
  }

  .medication-input input {
    flex: 1;
    padding: 0.5rem;
    font-size: 1rem;
    border: 1px solid #ddd;
    border-radius: 5px;
    margin-right: 0.5rem;
  }

  .medication-input button {
    padding: 0.5rem 1rem;
    font-size: 1rem;
    color: white;
    background-color: #927458;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

  .medication-input button:hover {
    background-color: #755b3c;
  }

  .medication-list {
    list-style-type: none;
    padding: 0;
    margin: 0;
  }

  .medication-list li {
    display: flex;
    align-items: center;
    padding: 0.5rem;
    background: #ffffff;
    border-radius: 5px;
    margin-bottom: 0.5rem;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }

  .medication-list li.completed span {
    text-decoration: line-through;
    color: #888;
  }

  .medication-list li input[type="checkbox"] {
    margin-right: 0.5rem;
  }

  .medication-list li .delete-btn {
    margin-left: auto;
    background: transparent;
    border: none;
    color: #888;
    font-size: 1.2rem;
    cursor: pointer;
  }

  .medication-list li .delete-btn:hover {
    color: #ff4c4c;
  }
</style>
