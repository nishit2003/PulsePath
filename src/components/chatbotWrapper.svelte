<script>
  import { onMount } from "svelte";
  import Scheduler from "./Scheduler.svelte"; 
  import BouncingDots from "./BouncingsDots.svelte"; 

  let showChat = false; // Controls the visibility of the chat popup

  // Toggles the chat popup
  function toggleChat() {
    showChat = !showChat;
  }
</script>

<div>
  <!-- Round Button -->
  <button class="chat-toggle" on:click={toggleChat}>
    💬
  </button>

  <!-- Chat Popup -->
  {#if showChat}
    <div class="chat-popup">
      <div class="chat-header">
        <h2>Chat with PulsePath AI</h2>
        <button class="close-btn" on:click={toggleChat}>×</button>
      </div>
      <div class="chat-body">
        <Scheduler />
      </div>
    </div>
  {/if}
</div>

<style>
  /* Round button styling */
  .chat-toggle {
    position: fixed;
    bottom: 20px;
    left: 20px;
    width: 60px;
    height: 60px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.5rem;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.2);
    cursor: pointer;
    transition: transform 0.3s ease, background-color 0.3s ease;
  }

  .chat-toggle:hover {
    background-color: #0056b3;
    transform: scale(1.1);
  }

  /* Chat popup styling */
  .chat-popup {
    position: fixed;
    bottom: 100px;
    left: 20px;
    width: 360px;
    max-height: 70vh;
    background-color: #f8f9fa;
    border-radius: 12px;
    box-shadow: 0px 6px 15px rgba(0, 0, 0, 0.2);
    display: flex;
    flex-direction: column;
    overflow: hidden;
    animation: fadeIn 0.3s ease-out;
  }

  .chat-header {
    background-color: #007bff;
    color: white;
    padding: 10px 15px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-top-left-radius: 12px;
    border-top-right-radius: 12px;
  }

  .chat-header h2 {
    font-size: 1.2rem;
    margin: 0;
  }

  .close-btn {
    background: none;
    color: white;
    border: none;
    font-size: 1.5rem;
    cursor: pointer;
  }

  .chat-body {
    padding: 10px;
    overflow-y: auto;
    flex: 1;
    display: flex;
    flex-direction: column;
  }

  /* Animation for popup */
  @keyframes fadeIn {
    from {
      opacity: 0;
      transform: translateY(20px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
</style>
