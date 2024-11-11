<!-- src/components/ChangeDate.svelte -->
<script>
  import { Modal, Button } from "flowbite-svelte";

  export let showModal = false;
  export let onClose;

  // State to hold the selected date
  let selectedDate = new Date().toISOString().substring(0, 10); // Default to today’s date

  function saveDate() {
    console.log("Selected Date:", selectedDate); // Replace with actual save logic if needed
    onClose(); // Close the modal
  }
</script>

<Modal open={showModal} on:close={onClose} placement="center">
  <div class="change-date-container">
    <h1 class="modal-title">Change Date</h1>
    <div class="date-picker">
      <label for="date">Select Date:</label>
      <input
        type="date"
        id="date"
        bind:value={selectedDate}
        min="2020-01-01"
        max="2030-12-31"
      />
    </div>
    <Button color="light" class="save-btn mt-4" on:click={saveDate}>Save Date</Button>
  </div>
</Modal>

<style>
  .change-date-container {
    padding: 2rem;
    background: #ffffff;
    border-radius: 20px;
    box-shadow: 0px 5px 15px rgba(0, 0, 0, 0.1);
    text-align: center;
    max-width: 400px;
    margin: 1rem auto;
  }

  .modal-title {
    font-size: 1.8rem;
    color: #4a4a4a;
    font-weight: bold;
    margin-bottom: 1.5rem;
  }

  .date-picker {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 1rem;
  }

  .date-picker label {
    font-size: 1rem;
    color: #555;
    margin-bottom: 0.5rem;
  }

  .date-picker input {
    padding: 0.5rem;
    border: 1px solid #ddd;
    border-radius: 8px;
    text-align: center;
    font-size: 1rem;
  }

  .save-btn {
    font-size: 1rem;
    background-color: #007bff;
    color: white;
    border-radius: 10px;
    transition: background 0.3s;
  }

  .save-btn:hover {
    background-color: #0056b3;
  }
</style>
