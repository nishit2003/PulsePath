<script>
  // Add any additional logic here if needed
</script>

<style>
  :global(body) {
    margin: 0;
    scroll-behavior: smooth;
    background-color: #E9EDC9; /* Base background color */
    font-family: Arial, sans-serif;
    color: #333;
  }

  .container {
    margin-left: 110px;
    /* background-color: #E9EDC9; Soft cream */
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 20px;
    width: 100%;
    height: 100vh;
  }

  .content {
    display: flex;
    flex-direction: column;
    align-items: center;
    max-width: 1200px;
    width: 100%;
    color: #333;
  }

  h1 {
    font-size: 2.5rem;
    margin-bottom: 10px;
    font-weight: bold;
    color: #D4A373; /* Warm caramel for headers */
  }

  p {
    font-size: 1.2rem;
    margin-bottom: 30px;
    line-height: 1.5;
    color: #555; /* Softer dark text */
  }

  .steps {
    display: flex;
    flex-direction: column;
    gap: 20px;
    flex: 1;
    margin-right: 50px;
  }

  .step h2 {
    font-size: 1.5rem;
    margin-bottom: 10px;
    font-weight: bold;
    color: #D4A373; /* Warm caramel */
  }

  .step p {
    font-size: 1rem;
    line-height: 1.5;
    color: #555;
  }

  .image {
    display: flex;
    flex-direction: column;
    align-items: center;
    flex: 1;
    max-width: 600px;
    width: 100%;
  }

  img {
    width: 100%;
    height: auto;
    border-radius: 10px;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1); /* Subtle shadow */
  }

  .buttons {
    display: flex;
    justify-content: center;
    gap: 15px;
    margin-top: 20px;
  }

  .button {
    padding: 10px 20px;
    font-size: 1rem;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-weight: bold;
    color: #FAEDCD; /* Soft beige text */
    background-color: #D4A373; /* Warm caramel */
    text-decoration: none;
    transition: background-color 0.3s ease, transform 0.2s;
  }

  .button:hover {
    background-color: #f5ebe2; /* Lighter cream hover */
    color: #333;
    transform: translateY(-2px); /* Slight lift effect */
  }

  @media (min-width: 768px) {
    .content {
      flex-direction: row;
      gap: 50px;
      text-align: left;
    }

    .steps {
      align-items: flex-start;
    }
  }
</style>

<div class="container">
  <div class="content">
    <div class="steps">
      <h1>Start your journey today</h1>
      <p>
        Journaling is a proven way to completely change your life, especially when you stick with it over time.
        Each time you write, you'll get unparalleled clarity and life perspective.
      </p>
      <div class="step">
        <h2>1. Start writing</h2>
        <p>All you have to do is start. Take 5 minutes to write in your journal about how you're feeling or reflect on the day.</p>
      </div>
      <div class="step">
        <h2>2. Keep it going</h2>
        <p>The more you write, the easier it will be. Set reminders to keep a regular daily, weekly, or monthly cadence.</p>
      </div>
      <div class="step">
        <h2>3. Reflect and grow</h2>
        <p>Links to your entries will be sent to you in the future so you can see through a clear window into the past.</p>
      </div>
    </div>
    <div class="image">
      <img src="https://images.squarespace-cdn.com/content/v1/621d0ecdf113087234bcbd97/bc30aade-84dc-4e65-abe4-7fa658caeb54/pexels-karolina-grabowska-4476376.jpg" alt="Journaling" />
      <div class="buttons">
        <a href="#pricing" class="button">View Pricing</a>
        <a href="#mood" class="button">Start Journaling Now</a>
      </div>
    </div>
  </div>
</div>
