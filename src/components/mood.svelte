<!-- src/components/MoodTracker.svelte -->
<script>
  let moodOptions = [
    { emoji: '😊', description: 'Happy' },
    { emoji: '😐', description: 'Neutral' },
    { emoji: '😢', description: 'Sad' },
    { emoji: '😠', description: 'Angry' },
    { emoji: '😴', description: 'Tired' }
  ];
  
  let selectedMood = null;
  let moodHistory = [];

  function logMood() {
    if (selectedMood) {
      // Log time instead of date
      const time = new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
      moodHistory = [...moodHistory, { ...selectedMood, time }];
      selectedMood = null; // Clear selection after logging
    }
  }

  function selectMood(mood) {
    selectedMood = mood;
  }
</script>

<div class="mood-tracker">
  <h2>Log Your Mood</h2>
  <div class="mood-options">
    {#each moodOptions as mood}
      <div
        class="mood-option {selectedMood === mood ? 'selected' : ''}"
        on:click={() => selectMood(mood)}
      >
        <span class="emoji">{mood.emoji}</span>
        <span class="description">{mood.description}</span>
      </div>
    {/each}
  </div>
  <button class="log-button" on:click={logMood}>Log Mood</button>

  <h3>Mood History</h3>
  <ul class="mood-history">
    {#each moodHistory as entry}
      <li>{entry.time} - {entry.emoji} {entry.description}</li>
    {/each}
  </ul>
</div>

<style>
  .mood-tracker {
    background: #f7f7f7;
    padding: 1.5rem;
    border-radius: 30px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    margin-bottom: 2rem;
    width: 400px;
    margin-left: 15px;
  }

  h2 {
    font-size: 1.5rem;
    color: #4a4a4a;
    margin-bottom: 1rem;
    text-align: center;
  }

  .mood-options {
    display: flex;
    gap: 1rem;
    justify-content: space-around;
    margin-bottom: 1rem;
    flex-wrap: wrap;
  }

  .mood-option {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 0.5rem;
    cursor: pointer;
    background: #ffffff;
    border-radius: 8px;
    transition: transform 0.2s, background-color 0.2s;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    width: 70px;
  }

  .mood-option.selected {
    background-color: #b2ebf2;
    transform: scale(1.1);
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
  }

  .emoji {
    font-size: 2rem;
  }

  .description {
    font-size: 0.9rem;
    color: #4a4a4a;
    margin-top: 0.3rem;
  }

  .log-button {
    padding: 0.5rem 1rem;
    font-size: 1rem;
    color: white;
    background-color: #e1c5a1;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
    display: block;
    margin: 0 auto;
  }

  .log-button:hover {
    background-color: #917359;
  }

  h3 {
    font-size: 1.3rem;
    color: #4a4a4a;
    margin-top: 1.5rem;
    text-align: center;
  }

  .mood-history {
    list-style-type: none;
    padding: 0;
    margin: 0;
    text-align: left;
    max-height: 100px;
    overflow-y: auto;
  }

  .mood-history li {
    font-size: 1rem;
    color: #333;
    background: #e0f2f1;
    padding: 0.5rem;
    margin: 0.3rem 0;
    border-radius: 5px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }
</style>
