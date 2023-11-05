<script>
  let selectedOptions = []; // Change to an array to hold multiple selections

  function selectOption(option) {
    const index = selectedOptions.indexOf(option);
    if (index < 0) {
      selectedOptions = [...selectedOptions, option]; // Add to selections
    } else {
      selectedOptions = selectedOptions.filter((o) => o !== option); // Remove from selections
    }
  }

  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();

  function nextQuestion() {
    dispatch('next', { selectedOptions }); // Pass selectedOptions as a parameter
  }

  function previousQuestion() {
    dispatch('previous'); // Dispatches the 'previous' event to the parent
  }

  const question = "Select some mini money moves you could crush this week to boost that savings game?";
  const options = [
    'Whipping up your own killer lunch creations — who needs overpriced salads, anyway?',
    'Trading that barista shoutout for a homebrew — your wallet (and your kitchen skills) will thank you.',
    'Choosing kicks over cabs — turn that commute into your cardio and keep that coin.',
    'Hitting \'unsubscribe\' on a meh service — because who needs to pay for stuff they barely use?',
    'Skipping the impulse online buys — pause and picture your bank balance saying, \'We good.\'',
    'Going DIY with your entertainment — think movie night in or a home-spa sesh.',
    'Doing a closet cleanse and flipping your finds online — your style could be someone’s treasure (and your next deposit).',
    'Opting for a \'no-spend\' day — challenge yourself to spend zero cash and watch the savings stack.'
  ];
</script>

<style>
@keyframes slideIn {
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
  .question-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    position: relative;
    top: 0;
    left: 0;
    color: white;
  }

  .question-text {
    max-width: 80%;
    margin: 0 auto;
    padding: 20px;
    text-align: center;
    line-height: 1.5;
    color: white;
  }

  .option-button {
    margin: 10px;
    padding: 10px 20px;
    font-size: 16px;
    cursor: pointer;
    border: 2px solid transparent;
    border-radius: 20px;
    opacity: 0;
    transform: translateY(-100px);
    animation: slideIn 0.5s ease forwards;
    animation-delay: var(--animation-delay);
    background-color:black;
    color:white;
  }

  .option-button:hover {
    color: white;
    background-color: rgb(100,0,100);
    transition: background-color 0.125s, color 0.125s;
  }

  .option-button.selected {
    color: white;
    background-color: rgb(100,0,100);
  }

  .continue-button {
    padding: 10px 20px;
    font-size: 20px;
    background-color: #fff;
    cursor: pointer;
    border-radius: 25px;
    margin-top: 20px;
    background-color:black;
    color:white;
    border:none;
  }

  .continue-button:hover {
    color: white;
    background-color: rgb(100,0,100);
    transition: background-color 0.125s, color 0.125s;
  }

  @keyframes slideIn {
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  .navigation-buttons {
    display: flex;
    justify-content: center;
    gap: 20px; /* Adjust the gap as needed */
  }


  .back-button {
    padding: 10px 20px;
    font-size: 20px;
    cursor: pointer;
    background-color: #fff;
    border-radius: 25px;
    margin-top: 20px;
    background-color:black;
    color:white;
    border:none;
  }

  .back-button:hover {
    color: white;
    background-color: rgb(100,0,100);
    transition: background-color 0.125s, color 0.125s;
  }
</style>

<div class="question-container">
  <div class="question-text">
    <h1>{question}</h1>
  </div>
  {#each options as option, index}
    <button
      class="option-button {selectedOptions.includes(option) ? 'selected' : ''}"
      on:click={() => selectOption(option)}
      style="--animation-delay: {index * 100}ms;">
      {option}
    </button>
  {/each}
  <div class="navigation-buttons">
    <button class="back-button" on:click={previousQuestion}>←</button>
    <button class="continue-button" on:click={nextQuestion}>→</button>
  </div>
</div>
