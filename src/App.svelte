<script>
  import { writable } from 'svelte/store';
  import LoginScreen from './LoginScreen.svelte';
  import PersonalityTestQ1 from './PersonalityTestQ1.svelte';
  import PersonalityTestQ2 from './PersonalityTestQ2.svelte';
  import PersonalityTestQ3 from './PersonalityTestQ3.svelte';
  import PersonalityTestQ4 from './PersonalityTestQ4.svelte';
  import PersonalityTestQ5 from './PersonalityTestQ5.svelte';

  const currentQuestionIndex = writable(-1); // Start with -1 to show login screen first
  const totalQuestions = 5;

  function handleLogin() {
    currentQuestionIndex.set(0); // Start the test at the first question after login
  }

  function goToNextQuestion() {
    currentQuestionIndex.update(n => (n + 1 < totalQuestions ? n + 1 : n));
  }

  // New function to move to the previous question
  function goToPreviousQuestion() {
    currentQuestionIndex.update(n => (n > 0 ? n - 1 : n));
  }
</script>

<!-- Inside your parent component's markup -->
{#if $currentQuestionIndex === -1}
  <LoginScreen on:login={handleLogin} />
{:else if $currentQuestionIndex === 0}
  <PersonalityTestQ1 on:next={goToNextQuestion} on:previous={goToPreviousQuestion} />
{:else if $currentQuestionIndex === 1}
  <PersonalityTestQ2 on:next={goToNextQuestion} on:previous={goToPreviousQuestion} />
{:else if $currentQuestionIndex === 2}
  <PersonalityTestQ3 on:next={goToNextQuestion} on:previous={goToPreviousQuestion} />
{:else if $currentQuestionIndex === 3}
  <PersonalityTestQ4 on:next={goToNextQuestion} on:previous={goToPreviousQuestion} />
{:else if $currentQuestionIndex === 4}
  <PersonalityTestQ5 on:next={goToNextQuestion} on:previous={goToPreviousQuestion} />
{/if}