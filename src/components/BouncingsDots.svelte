<script>
  // No additional JavaScript needed for this component
</script>

<div class="bouncing-dots-container">
  <div class="dot dot1"></div>
  <div class="dot dot2"></div>
  <div class="dot dot3"></div>
</div>

<style>
  /* Main container for the bouncing dots */
  .bouncing-dots-container {
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    width: 50px; /* Adjust width for dot spacing */
    height: 20px; /* Height of the bouncing animation area */
  }

  /* Shared styles for each dot */
  .dot {
    width: 10px;
    height: 10px;
    background-color: #007bff; /* Dot color */
    border-radius: 50%; /* Makes the dots circular */
    animation: bounce 1.2s infinite ease-in-out;
  }

  /* Adding delay for each dot to create the bouncing effect */
  .dot1 {
    animation-delay: 0s;
  }

  .dot2 {
    animation-delay: 0.2s;
  }

  .dot3 {
    animation-delay: 0.4s;
  }

  /* Bouncing animation keyframes */
  @keyframes bounce {
    0%, 100% {
      transform: translateY(0); /* Initial and final position */
    }
    50% {
      transform: translateY(-10px); /* Move up */
    }
  }
</style>
