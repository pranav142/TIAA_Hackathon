<script>
  let selectedOption = null; // Holds a single selected option

  function selectOption(option) {
    selectedOption = option; // Assign selected option directly
  }

  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();

  function nextQuestion() {
    dispatch('next', { selectedOption }); // Pass selectedOption as a parameter
  }

  function previousQuestion() {
    dispatch('previous'); // Dispatches the 'previous' event to the parent
  }

    function submitAnswers() {
    // Here you can do something with the selectedOptions if needed
    dispatch('finish'); // Dispatches an event to signal the completion of the quiz
  }

  const question = "How do you feel about debt? Pick one statement that feels most like your financial style.";
  const options = [
    'I ghost debt like a bad date — if I can\'t pay cash, I\'m out.',
    'Debt\'s chill if we\'re talking manageable numbers — I\'m not about that over-the-top life.',
    'I\'m playing 4D chess with my cash — debt\'s a strategy, not a scare.',
    'Not gonna lie, sometimes debt feels like that messy roommate I can\'t shake.'
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
  }

  .question-text {
    max-width: 80%;
    margin: 0 auto;
    padding: 20px;
    text-align: center;
    line-height: 1.5;
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
      class="option-button {selectedOption === option ? 'selected' : ''}"
      on:click={() => selectOption(option)}
      style="--animation-delay: {index * 100}ms;">
      {option}
    </button>
  {/each}
  <div class="navigation-buttons">
    <button class="back-button" on:click={previousQuestion}>←</button>
    {#if selectedOption} <!-- Check if selectedOption is not null -->
      <button class="continue-button" on:click={submitAnswers}>Finish</button>
    {/if}
  </div>
</div>
