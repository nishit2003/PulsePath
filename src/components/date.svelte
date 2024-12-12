<script>
  import { Modal, Button } from "flowbite-svelte";

  export let showModal = false;
  export let onClose;

  // State to hold the selected date
  let selectedDate = new Date().toISOString().substring(0, 10); // Default to today’s date

  function handleSubmit() {
    const randomOutput = Math.random() > 0.5; // Simulate whether data exists

    if (randomOutput) {
      alert("Entries for that date retrieved successfully!");
    } else {
      alert("No data exists for that date.");
    }
    onClose(); // Close the modal
  }
</script>

<Modal open={showModal} on:close={onClose} placement="center">
  <div class="change-date-container">
    <h1 class="modal-title">Want to change the date of login?</h1>

    <div class="date-picker">
      <label for="date">Select a new date:</label>
      <input
        type="date"
        id="date"
        bind:value={selectedDate}
        min="2020-01-01"
        max="2030-12-31"
      />
    </div>

    <Button color="light" class="submit-btn mt-4" on:click={handleSubmit}>Submit</Button>

    <p class="note mt-4">* The output is random since we actually don’t have a database to store the data.</p>
  </div>
</Modal>

<style>
  .change-date-container {
    padding: 2rem;
    background: linear-gradient(145deg, #f5f5dc, #fff8dc);
    border-radius: 12px;
    box-shadow: 0px 6px 15px rgba(0, 0, 0, 0.1);
    text-align: center;
    max-width: 400px;
    margin: 0 auto;
    font-family: 'Arial', sans-serif;
  }

  .modal-title {
    font-size: 1.5rem;
    font-weight: 600;
    margin-bottom: 1rem;
    color: #3e2723;
  }

  .date-picker {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 1.5rem;
  }

  .date-picker label {
    font-size: 1rem;
    margin-bottom: 0.5rem;
    color: #6d4c41;
  }

  .date-picker input {
    padding: 0.5rem;
    border: 1px solid #d2b48c;
    border-radius: 8px;
    font-size: 1rem;
    width: 100%;
    max-width: 250px;
    background-color: #fffaf0;
    color: #3e2723;
  }

  .submit-btn {
    font-size: 1rem;
    padding: 0.5rem 1rem;
    border-radius: 8px;
    background-color: #d2b48c;
    color: white;
    font-weight: 600;
    transition: background-color 0.2s ease;
  }

  .submit-btn:hover {
    background-color: #b8860b;
  }

  .note {
    font-size: 0.875rem;
    color: #8b4513;
    margin-top: 1rem;
  }
</style>
