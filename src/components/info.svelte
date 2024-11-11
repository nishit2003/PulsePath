<!-- src/components/InfoModal.svelte -->
<script>
  import { Modal, Button } from "flowbite-svelte";

  export let showModal = false;
  export let onClose;
</script>

<Modal open={showModal} on:close={onClose} placement="center">
  <div class="info-container">
    <h1 class="info-title">📋 How to Use PulsePath</h1>
    <ul class="info-list">
      <li class="info-item">
        <strong>📋 User Profile:</strong> View and update your personal health info, including height, weight, and BMI. Click "Edit" to update and save changes.
      </li>
      <li class="info-item">
        <strong>🎯 Set Goals:</strong> Define daily targets for sleep, water intake, steps, and calories. Update anytime to match your health goals.
      </li>
      <li class="info-item">
        <strong>📅 Change Date:</strong> Use this feature to view your health data for different dates, allowing you to track progress over time.
      </li>
      <li class="info-item">
        <strong>💡 Health Tips:</strong> Access random wellness tips to stay motivated. Click "New Tips" to refresh and get more advice.
      </li>
      <li class="info-item">
        <strong>📈 Track Progress:</strong> Log your mood, steps, water intake, and other activities in the dashboard. Monitor your achievements daily!
      </li>
    </ul>
    <Button color="light" class="close-btn mt-4" on:click={onClose}>Close</Button>
  </div>
</Modal>

<style>
  .info-container {
    padding: 2.5rem;
    background: #fff7e6;
    border-radius: 20px;
    box-shadow: 0px 10px 25px rgba(0, 0, 0, 0.15);
    text-align: center;
    max-width: 500px;
    margin: 1rem auto;
  }

  .info-title {
    font-size: 2rem;
    color: #6e5c41;
    font-weight: bold;
    margin-bottom: 1.5rem;
    display: flex;
    align-items: center;
    justify-content: center;
    animation: fadeIn 0.6s ease;
  }

  .info-list {
    list-style-type: none;
    padding: 0;
    margin: 0;
    color: #4a4a4a;
    text-align: left;
    max-height: 500px;
    overflow-y: auto;
  }

  .info-item {
    background: #fef5d4;
    padding: 1rem;
    margin-bottom: 0.8rem;
    border-radius: 12px;
    color: #4a4a4a;
    font-size: 1rem;
    box-shadow: 0 3px 10px rgba(0, 0, 0, 0.05);
    transition: transform 0.3s;
  }

  .info-item:hover {
    transform: translateY(-3px);
    background: #ffebb5;
  }

  .close-btn {
    font-size: 1rem;
    background-color: #ffd36b;
    border-radius: 12px;
    color: #4a4a4a;
    padding: 0.5rem 1.5rem;
    margin-top: 1rem;
    font-weight: bold;
    transition: background-color 0.3s, transform 0.2s;
  }

  .close-btn:hover {
    background-color: #ffcb4d;
    transform: scale(1.05);
  }

  @keyframes fadeIn {
    0% { opacity: 0; }
    100% { opacity: 1; }
  }
</style>
