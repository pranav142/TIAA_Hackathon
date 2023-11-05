<script>
  import { writable } from 'svelte/store';
  import LoginScreen from './LoginScreen.svelte';
  import PersonalityTestQ1 from './PersonalityTestQ1.svelte';
  import PersonalityTestQ2 from './PersonalityTestQ2.svelte';
  import PersonalityTestQ3 from './PersonalityTestQ3.svelte';
  import PersonalityTestQ4 from './PersonalityTestQ4.svelte';
  import PersonalityTestQ5 from './PersonalityTestQ5.svelte';
  import MainPage from './MainPage.svelte';

  const currentQuestionIndex = writable(-1); // Start with -1 to show login screen first
  const totalQuestions = 5; // Total questions before showing the main page

  function handleLogin() {
    currentQuestionIndex.set(0); // Start the test at the first question after login
  }

  function goToNextQuestion() {
    currentQuestionIndex.update(n => {
      if (n + 1 === totalQuestions) {
        // If the current question is the last one, move to the main page
        return n + 1;
      } else if (n < totalQuestions) {
        // Otherwise, proceed to the next question
        return n + 1;
      } else {
        return n; // If at the main page already, do nothing
      }
    });
  }

  // New function to move to the previous question
  function goToPreviousQuestion() {
    currentQuestionIndex.update(n => (n > 0 ? n - 1 : n));
  }

   function handleFinish() {
    currentQuestionIndex.set(totalQuestions); // This sets the index to 5, moving to the main page
  }
</script>

{#if $currentQuestionIndex === -1}
  <LoginScreen on:login={handleLogin} />
{:else if $currentQuestionIndex >= 0 && $currentQuestionIndex < totalQuestions}
  {#if $currentQuestionIndex === 0}
    <PersonalityTestQ1 on:next={goToNextQuestion} on:previous={goToPreviousQuestion} />
  {:else if $currentQuestionIndex === 1}
    <PersonalityTestQ2 on:next={goToNextQuestion} on:previous={goToPreviousQuestion} />
  {:else if $currentQuestionIndex === 2}
    <PersonalityTestQ3 on:next={goToNextQuestion} on:previous={goToPreviousQuestion} />
  {:else if $currentQuestionIndex === 3}
    <PersonalityTestQ4 on:next={goToNextQuestion} on:previous={goToPreviousQuestion} />
  {:else if $currentQuestionIndex === 4}
    <PersonalityTestQ5 on:finish={handleFinish} on:previous={goToPreviousQuestion} />
  {/if}
{:else if $currentQuestionIndex === totalQuestions}
  <MainPage />
{/if}