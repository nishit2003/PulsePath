<!-- src/components/HealthTips.svelte -->
<script>
  import { Modal, Button } from "flowbite-svelte"; // Import Modal from Flowbite
  
  export let tips = [
    "Stay hydrated! Aim for at least 8 cups of water each day.",
    "Aim for 7-8 hours of quality sleep every night for optimal health.",
    "Keep active! Try to exercise for at least 30 minutes daily.",
    "Remember to log your meals and daily mood to track progress.",
    "Eat a variety of colorful fruits and vegetables for essential vitamins.",
    "Take a short walk every hour to reduce the health risks of prolonged sitting.",
    "Avoid sugary drinks; opt for water or herbal teas instead.",
    "Incorporate strength training exercises twice a week to build muscle.",
    "Practice mindfulness or meditation to reduce stress.",
    "Include fiber-rich foods like oats, beans, and whole grains in your diet.",
    "Practice deep breathing exercises to improve lung capacity and relaxation.",
    "Choose whole foods over processed ones whenever possible.",
    "Limit screen time before bed to improve sleep quality.",
    "Eat smaller, more frequent meals to keep your energy levels steady.",
    "Use a standing desk or take breaks to stretch if you work at a computer.",
    "Try to get some natural sunlight exposure every morning for better mood and sleep.",
    "Incorporate healthy fats like olive oil, nuts, and avocado into your diet.",
    "Avoid late-night snacks to allow for better digestion during sleep.",
    "Focus on posture and do simple stretches throughout the day to prevent back pain.",
    "Stay socially connected to boost mental health and reduce feelings of loneliness.",
    "Set realistic and achievable health goals to stay motivated.",
    "Limit caffeine intake in the afternoon to avoid disrupting sleep.",
    "Practice gratitude daily for better mental health and resilience.",
    "Include lean proteins like fish, chicken, and legumes in your meals.",
    "Stay consistent with your health habits, even on weekends or holidays.",
    "Get regular health check-ups to stay on top of your wellness journey.",
    "Limit screen exposure to reduce eye strain, especially at night.",
    "Use smaller plates to control portion sizes and prevent overeating.",
    "Take time to enjoy your meals without distractions for better digestion.",
    "Practice good hygiene and wash your hands regularly to avoid infections.",
    "Make time for hobbies and activities you enjoy to boost mental wellness.",
    "Avoid comparing your fitness journey to others; focus on your own progress.",
    "Incorporate a variety of exercises to avoid boredom and work different muscles.",
    "Reduce sodium intake to support heart health and reduce bloating.",
    "Practice a wind-down routine in the evening to help signal your body for sleep.",
    "Laugh often – it’s great for your mood and mental well-being!",
    "Use a food journal to track your intake and make mindful choices.",
    "Stand up and stretch every 20 minutes to keep your muscles relaxed.",
    "Cook more meals at home to have better control over ingredients and portions.",
    "Learn to say no to activities that drain you and focus on self-care.",
    "Don’t skip meals; aim for a balanced breakfast, lunch, and dinner.",
    "Stay curious and keep learning about health and wellness to stay motivated.",
    "Limit alcohol intake to support liver health and maintain energy.",
    "Experiment with new recipes to make healthy eating enjoyable.",
    "Stay positive and remember that small changes add up to big results over time."
  ];
  
  export let showModal = false;
  export let onClose; // Function to close the modal

  // Random tips array to display
  let randomTips = [];

  // Function to generate 5 random tips
  function getRandomTips() {
    randomTips = tips.sort(() => 0.5 - Math.random()).slice(0, 5);
  }

  // Watch for showModal change and refresh tips on open
  $: if (showModal) {
    getRandomTips();
  }
</script>

<Modal open={showModal} on:close={onClose} placement="center">
  <div class="tips-container">
    <h1 class="tips-title">Health Tips</h1>
    <ul class="tips-list">
      {#each randomTips as tip}
        <li class="tip-item">{tip}</li>
      {/each}
    </ul>
    <Button color="light" class="close-btn mt-4" on:click={onClose}>Close</Button>
  </div>
</Modal>

<style>
  .tips-container {
    padding: 2rem;
    background: #ffffff;
    border-radius: 20px;
    box-shadow: 0px 5px 15px rgba(0, 0, 0, 0.1);
    text-align: center;
    max-width: 500px;
    margin: 1rem auto;
  }

  .tips-title {
    font-size: 1.8rem;
    color: #4a4a4a;
    font-weight: bold;
    margin-bottom: 1.5rem;
  }

  .tips-list {
    list-style-type: none;
    padding: 0;
    margin: 0;
  }

  .tip-item {
    font-size: 1rem;
    margin-bottom: 0.7rem;
    padding: 0.7rem;
    background: #e8f5e9;
    border-radius: 10px;
    color: #333;
    transition: transform 0.3s;
  }

  .tip-item:hover {
    transform: translateY(-3px);
  }

  .close-btn {
    font-size: 1rem;
    background-color: #007bff;
    border-radius: 10px;
    color: white;
    transition: background 0.3s;
  }

  .close-btn:hover {
    background-color: #0056b3;
  }
</style>
