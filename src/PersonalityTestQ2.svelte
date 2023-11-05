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

  const question = "What are those life moments you're looking forward to the most? Feel free to mix and match; your future's just as customizable as your playlist.";
  const options = [
    'Jet-setting or discovering hidden local gems — every journey\'s an epic story.',
    'Leveling up your hobbies or sports game — from side hustle to spotlight.',
    'Building a vault of epic family tales and traditions.',
    'Making a mark in your community or on the world stage.',
    'Expanding your mind and skills in ways that would make your bio epic.',
    'Crafting a home vibe that\'s all chill, comfort, and style.',
    'Launching or scaling that dream project that’s going to be your legacy.'
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
