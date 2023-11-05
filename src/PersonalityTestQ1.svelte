<script>
  let selectedOptions = []; // Use an array to track selected options

  function selectOption(option) {
    const index = selectedOptions.indexOf(option);
    if (index < 0) {
      selectedOptions = [...selectedOptions, option]; // Add to the array
    } else {
      selectedOptions = selectedOptions.filter((o) => o !== option); // Remove from the array
    }
  }

  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();

  function nextQuestion() {
    dispatch('next', { selectedOptions }); // Pass the selected options on
  }

  function previousQuestion() {
    dispatch('previous'); // Dispatch a 'previous' event when back arrow is clicked
  }

  const question = "When it comes to stacking your savings, what's the big dream driving you?";
  const options = [
    'Locking down that stress-free future where you\'re totally covered.',
    'Globetrotting to bucket-list spots and soaking up every culture.',
    'Setting up your fam with the best — because they mean everything.',
    'Hitting that level of cash flow where you call all the shots.',
    'Crushing those financial milestones and celebrating every win.'
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
  <h1>{question}</h1>
  {#each options as option, index}
    <button
      class="option-button {selectedOptions.includes(option) ? 'selected' : ''}"
      on:click={() => selectOption(option)}
      style="--animation-delay: {index * 100}ms;">
      {option}
    </button>
  {/each}
  <!-- Back button -->
   <div class="navigation-buttons">
    <button class="back-button" on:click={previousQuestion}>←</button>
    <button class="continue-button" on:click={nextQuestion}>→</button>
  </div>
</div>
