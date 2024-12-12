<script>
  import BouncingDots from "./BouncingsDots.svelte"; // Import the typing indicator
  import { onMount } from "svelte";

  export let data = [
  { text: "Hi there! Welcome to your personalized assistant.", who: "them" },
  { text: "I'm here to guide you and learn more about your preferences.", who: "them" },
  { text: "Let's start with a quick discovery session.", who: "them" },
  { text: "What's your favorite way to start the day?", who: "them" },
  { text: "Good morning! I like to start with a nice breakfast.", who: "you" },
  { text: "That's a great start! A healthy morning sets the tone for the day.", who: "them" },
  { text: "Now, let’s talk about your goals.", who: "them" },
  { text: "What are you currently working toward?", who: "them" },
  { text: "I'm focused on improving my productivity and time management.", who: "you" },
  { text: "Excellent! Here are a few tips you might find helpful:", who: "them" },
  { text: "1. Prioritize your tasks with the Eisenhower Matrix.", who: "them" },
  { text: "2. Break large tasks into smaller, manageable steps.", who: "them" },
  { text: "3. Remember to schedule breaks to stay fresh and focused.", who: "them" },
  { text: "Thanks, those tips sound great!", who: "you" },
  { text: "You're welcome! Let’s discuss your long-term aspirations.", who: "them" },
  { text: "Where do you see yourself in 5 years?", who: "them" },
  { text: "I see myself leading a team and making a positive impact.", who: "you" },
  { text: "That's inspiring! Leadership requires continuous growth.", who: "them" },
  { text: "How do you currently build your skills and knowledge?", who: "them" },
  { text: "I enjoy reading, taking courses, and learning from mentors.", who: "you" },
  { text: "Fantastic approach! Combining theory and experience is key.", who: "them" },
  { text: "Let’s touch on one more important aspect: collaboration.", who: "them" },
  { text: "How do you approach working with others in a team?", who: "them" },
  { text: "I believe in open communication and shared responsibility.", who: "you" },
  { text: "That’s great to hear! Teamwork makes the dream work.", who: "them" },
  { text: "Finally, is there anything specific you'd like assistance with?", who: "them" },
  { text: "Yes, I’d love help with structuring my daily schedule.", who: "you" },
  { text: "Absolutely! Here's a simple plan to start:", who: "them" },
  { text: "1. Allocate time blocks for high-priority tasks.", who: "them" },
  { text: "2. Reserve 30 minutes daily for personal development.", who: "them" },
  { text: "3. Reflect and adjust your plan at the end of the day.", who: "them" },
  { text: "Thank you! I’m excited to put this into action.", who: "you" },
  { text: "You're very welcome! Let me know if you need more tips.", who: "them" },
  { text: "Have a productive day ahead!", who: "them" },
];


  let current = []; // Messages currently displayed
  let isTyping = false; // Shows the typing indicator when the bot is preparing a message
  let currentIndex = 0; // Tracks the index of the next message to display

  // Function to calculate realistic typing delay based on text length
  function readingTime(text) {
    const wordsPerSecond = 225 / 60; // Approx. words per second
    const words = text.trim().split(/\s+/).length;
    const time = Math.ceil((words / wordsPerSecond) * 1000); // Convert to ms
    return time < 1500 ? 1500 : time; // Ensure a minimum delay of 1.5s
  }

  // Function to schedule and display messages
  function scheduleMessages() {
    if (currentIndex < data.length) {
      isTyping = true;

      // Simulate typing delay
      setTimeout(() => {
        current = [...current, data[currentIndex]]; // Add the next message
        currentIndex++;
        isTyping = false;

        // Schedule the next message
        if (currentIndex < data.length) {
          scheduleMessages();
        }
      }, readingTime(data[currentIndex].text));
    }
  }

  // Start scheduling messages when the component is mounted
  onMount(() => {
    scheduleMessages();
  });
</script>

<div class="scheduler">
  <!-- Render each message inline -->
  {#each current as { text, who }}
    <div class="message {who}">
      {text}
    </div>
  {/each}

  <!-- Typing indicator -->
  {#if isTyping}
    <div class="typing-indicator">
      <BouncingDots />
    </div>
  {/if}
</div>

<style>
  .scheduler {
    display: flex;
    flex-direction: column;
    gap: 10px;
    padding: 10px;
  }

  .message {
    padding: 10px 15px;
    border-radius: 10px;
    max-width: 75%;
    word-wrap: break-word;
  }

  .message.you {
    background-color: #007bff;
    color: white;
    align-self: flex-end;
  }

  .message.them {
    background-color: #f1f1f1;
    color: #333;
    align-self: flex-start;
  }

  .typing-indicator {
    margin-left: 10px;
    padding: 5px;
  }
</style>
