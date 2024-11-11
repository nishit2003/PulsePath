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
    <h1 class="modal-title">🗓️ Change Your Date</h1>
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
    <Button color="light" class="save-btn mt-4" on:click={saveDate}>✨ Save Date</Button>
  </div>
</Modal>

<style>
  .change-date-container {
    padding: 2.5rem;
    background: linear-gradient(145deg, #e3f2fd, #ffffff);
    border-radius: 20px;
    box-shadow: 0px 10px 25px rgba(0, 0, 0, 0.15);
    text-align: center;
    max-width: 400px;
    margin: 1rem auto;
    transition: transform 0.3s ease, background-color 0.3s ease;
  }

  .change-date-container:hover {
    transform: scale(1.02);
    background-color: #f8f9fa;
  }

  .modal-title {
    font-size: 2rem;
    color: #3a3a3a;
    font-weight: 600;
    margin-bottom: 1.5rem;
    display: flex;
    align-items: center;
    justify-content: center;
    animation: fadeIn 0.6s ease;
  }

  .date-picker {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 1.5rem;
    animation: slideIn 0.5s ease;
  }

  .date-picker label {
    font-size: 1.1rem;
    color: #333;
    margin-bottom: 0.5rem;
    font-weight: 500;
  }

  .date-picker input {
    padding: 0.6rem;
    border: 1px solid #bbb;
    border-radius: 8px;
    text-align: center;
    font-size: 1.1rem;
    box-shadow: 0px 3px 8px rgba(0, 0, 0, 0.1);
    transition: box-shadow 0.3s ease;
  }

  .date-picker input:focus {
    box-shadow: 0px 5px 15px rgba(0, 0, 0, 0.2);
  }

  .save-btn {
    font-size: 1.1rem;
    background-color: #6c63ff;
    color: #fff;
    border-radius: 15px;
    padding: 0.5rem 1.2rem;
    font-weight: bold;
    transition: background-color 0.3s ease, transform 0.2s ease;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .save-btn:hover {
    background-color: #594fbf;
    transform: scale(1.05);
  }

  @keyframes fadeIn {
    0% { opacity: 0; }
    100% { opacity: 1; }
  }

  @keyframes slideIn {
    0% { transform: translateY(20px); opacity: 0; }
    100% { transform: translateY(0); opacity: 1; }
  }
</style>
