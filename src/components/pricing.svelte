<script>
  let isYearly = true; // Toggle between monthly and yearly pricing
</script>

<style>
  .pricing-container {
    background-color: #fefae0;
    padding: 40px 20px;
    text-align: center;
    font-family: Arial, sans-serif;
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

<div id = "pricing" class="pricing-container">
  <h1>Choose your plan</h1>
  <p>PulsePath is always free but our Pro plans offer more flexibility, customization, and features to maximize your journaling experience.</p>

  <!-- Toggle for Monthly/Yearly -->
  <div class="toggle-container">
    <!-- <span>Pay Monthly</span> -->
    <div class="toggle" on:click={() => (isYearly = !isYearly)}>
      <span class={!isYearly ? 'active' : ''}>Pay Monthly</span>
      <span class={isYearly ? 'active' : ''}>Pay Yearly (-60%)</span>
    </div>
  </div>

  <!-- Plans -->
  <div class="plans">
    <!-- Basic Plan -->
    <div class="plan">
      <h2>Basic</h2>
      <p class="price">Free</p>
      <p>Get started with our free plan. No credit card required.</p>
      <ul class="features">
        <li>Unlimited entries</li>
        <li>Mobile apps</li>
        <li>Basic journal covers and fonts</li>
        <li>Simple writing reminders</li>
      </ul>
      <div class="cta">
        <button>Get started →</button>
      </div>
    </div>

    <!-- Pro Plan -->
    <div class="plan">
      <div class="most-popular">Most Popular</div>
      <h2>PulsePath Pro</h2>
      <p class="price">$19.99 <span>/ {isYearly ? "year" : "month"}</span></p>
      <p>Make it yours with customization, plus pro-active features to keep you writing.</p>
      <ul class="features">
        <li>Encryption locking</li>
        <li>Custom journal covers, fonts & colors</li>
        <li>Entry tagging</li>
        <li>PDF export</li>
        <li>Writing prompts</li>
        <li>Write via email (Penzu Post)</li>
      </ul>
      <div class="cta">
        <button>Go Pro →</button>
      </div>
    </div>

    <!-- Pro+ Plan -->
    <div class="plan">
      <h2>PulsePath Pro+</h2>
      <p class="price">$49.99 <span>/ {isYearly ? "year" : "month"}</span></p>
      <p>The most powerful suite of tools for journaling.</p>
      <ul class="features">
        <li>Premium handwritten fonts</li>
        <li>Fullscreen zen-mode</li>
        <li>Versions & entry recovery</li>
        <li>Premium support</li>
        <li>Military-grade encryption locking</li>
      </ul>
      <div class="cta">
        <button>Go Pro+ →</button>
      </div>
    </div>
  </div>
</div>
