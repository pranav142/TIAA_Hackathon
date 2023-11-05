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

  const question = "Pick out the goals that are worth hustling for";
  const options = [
    'Your own spot: A home that’s less about the \'gram and more about your sanctuary.',
    'Your ride: Think electric, high-tech, and ready for those road trip playlists.',
    'Your escape: Vacations that aren’t just breaks, but life-changing experiences.',
    'Your growth: An education fund because knowledge is not just power, it’s progress.',
    'Your security: A retirement fund that says \'later\' to the 9-to-5 grind.',
    'Your health: Insurance that’s less about the fine print, more about peace of mind.',
    'Your investment: Property that’s not just a space, but a smart move.'
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
    color: black;
  }

  .question-text {
    max-width: 80%;
    margin: 0 auto;
    padding: 20px;
    text-align: center;
    line-height: 1.5;
    color: black;
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
    cursor: pointer;
    background-color: #fff;
    border-radius: 25px;
    margin-top: 20px;
  }

  .continue-button:hover {
    color: white;
    background-color: rgb(100,0,100);
    transition: background-color 0.125s, color 0.125s;
  }

  .navigation-buttons {
    display: flex;
    justify-content: space-between;
    width: 50%; /* Adjust width as needed */
    margin: 20px auto; /* Centers the buttons with auto margins */
  }

  .back-button, .continue-button {
    padding: 10px 20px;
    font-size: 20px;
    cursor: pointer;
    background-color: #fff;
    border-radius: 25px;
    margin-top: 20px;
  }

  .back-button:hover, .continue-button:hover {
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
