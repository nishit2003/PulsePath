<script>
  let isYearly = true; // Toggle between monthly and yearly pricing

  // Pricing data
  const plans = [
    {
      name: "Basic",
      priceMonthly: "Free",
      priceYearly: "Free",
      description: "Get started with our free plan. No credit card required.",
      features: [
        "Unlimited entries",
        "Mobile apps",
        "Basic journal covers and fonts",
        "Simple writing reminders",
      ],
      cta: "Get started →",
      mostPopular: false,
    },
    {
      name: "PulsePath Pro",
      priceMonthly: "$19.99",
      priceYearly: "$79.99",
      description:
        "Make it yours with customization, plus pro-active features to keep you writing.",
      features: [
        "Encryption locking",
        "Custom journal covers, fonts & colors",
        "Entry tagging",
        "PDF export",
        "Writing prompts",
        "Write via email (Penzu Post)",
      ],
      cta: "Go Pro →",
      mostPopular: true,
    },
    {
      name: "PulsePath Pro+",
      priceMonthly: "$49.99",
      priceYearly: "$199.99",
      description: "The most powerful suite of tools for journaling.",
      features: [
        "Premium handwritten fonts",
        "Fullscreen zen-mode",
        "Versions & entry recovery",
        "Premium support",
        "Military-grade encryption locking",
      ],
      cta: "Go Pro+ →",
      mostPopular: false,
    },
  ];
</script>

<style>
  :global(html) {
    scroll-behavior: smooth;
  }
  .pricing-container {
    background-color: #cac389;
    padding: 40px 20px;
    text-align: center;
    font-family: Arial, sans-serif;
    height: 100vh;
  }

  h1 {
    font-size: 2.5rem;
    margin-bottom: 10px;
    font-weight: bold;
    color: #d4a373;
  }

  p {
    font-size: 1rem;
    color: #666;
    margin-bottom: 30px;
  }

  .toggle-container {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 10px;
    margin-bottom: 30px;
  }

  .toggle {
    display: flex;
    align-items: center;
    background-color: #e9edc9;
    border-radius: 20px;
    padding: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
  }

  .toggle span {
    font-size: 0.9rem;
    padding: 5px 10px;
  }

  .toggle .active {
    background-color: #d4a373;
    color: #fff;
    border-radius: 20px;
  }

  .plans {
    display: flex;
    justify-content: center;
    gap: 90px;
    flex-wrap: wrap;
  }

  .plan {
    background-color: #e9edc9;
    border-radius: 10px;
    padding: 20px;
    width: 300px;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
    text-align: left;
    position: relative;
  }

  .plan h2 {
    font-size: 1.5rem;
    margin-bottom: 10px;
    font-weight: bold;
  }

  .plan .price {
    font-size: 2rem;
    color: #d4a373;
    margin-bottom: 10px;
  }

  .plan .price span {
    font-size: 0.9rem;
    color: #666;
  }

  .plan p {
    margin-bottom: 15px;
    color: #555;
  }

  .features {
    list-style-type: none;
    padding: 0;
    margin-bottom: 20px;
  }

  .features li {
    margin-bottom: 10px;
    color: #333;
    display: flex;
    align-items: center;
  }

  .features li::before {
    content: "✔";
    margin-right: 10px;
    color: #d4a373;
  }

  .cta {
    text-align: center;
  }

  .cta button {
    background-color: #d4a373;
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    font-weight: bold;
    cursor: pointer;
    transition: background-color 0.3s;
  }

  .cta button:hover {
    background-color: #f5ebe2;
    color: #333;
  }

  .most-popular {
    position: absolute;
    top: -15px;
    left: 50%;
    transform: translateX(-50%);
    background-color: #faedcd;
    color: #d4a373;
    padding: 5px 10px;
    font-size: 0.9rem;
    font-weight: bold;
    border-radius: 20px;
  }
</style>

<div id="pricing" class="pricing-container">
  <h1>Choose your plan</h1>
  <p>
    PulsePath is always free but our Pro plans offer more flexibility,
    customization, and features to maximize your journaling experience.
  </p>

  <!-- Toggle for Monthly/Yearly -->
  <div class="toggle-container">
    <div class="toggle" on:click={() => (isYearly = !isYearly)}>
      <span class={!isYearly ? "active" : ""}>Pay Monthly</span>
      <span class={isYearly ? "active" : ""}>Pay Yearly (-60%)</span>
    </div>
  </div>

  <!-- Plans -->
  <div class="plans">
    {#each plans as plan}
      <div class="plan">
        {#if plan.mostPopular}
          <div class="most-popular">Most Popular</div>
        {/if}
        <h2>{plan.name}</h2>
        <p class="price">
          {isYearly ? plan.priceYearly : plan.priceMonthly}
          <span>/ {isYearly ? "year" : "month"}</span>
        </p>
        <p>{plan.description}</p>
        <ul class="features">
          {#each plan.features as feature}
            <li>{feature}</li>
          {/each}
        </ul>
        <div class="cta">
          <button>{plan.cta}</button>
        </div>
      </div>
    {/each}
  </div>
</div>
