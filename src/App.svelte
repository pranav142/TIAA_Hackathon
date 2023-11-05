<script>
  import { writable } from 'svelte/store';
  import LoginScreen from './LoginScreen.svelte';
  import PersonalityTestQ1 from './PersonalityTestQ1.svelte';
  import PersonalityTestQ2 from './PersonalityTestQ2.svelte';
  import PersonalityTestQ3 from './PersonalityTestQ3.svelte';
  import PersonalityTestQ4 from './PersonalityTestQ4.svelte';
  import PersonalityTestQ5 from './PersonalityTestQ5.svelte';
  import MainPage from './MainPage.svelte';
  import AvatarCreationPage from './AvatarCreationPage.svelte';

  const currentQuestionIndex = writable(-1); // Start with -1 to show login screen first
  const avatarCreationPageIndex = 5; // Index representing the avatar creation page
  const totalQuestions = 4; // Total questions in the personality test

  function handleLogin() {
	goToMainPage();
     // Start the test at the first question after login
  }

    function handleCreateAccount() {
    // Navigates directly to the MainPage after login
    currentQuestionIndex.set(0);
  }


  function goToNextQuestion() {
    currentQuestionIndex.update(n => n + 1);
  }

  function goToPreviousQuestion() {
    currentQuestionIndex.update(n => (n > 0 ? n - 1 : n));
  }

  function handleFinish() {
    currentQuestionIndex.set(avatarCreationPageIndex); // Move to the avatar creation page
  }

  function goToMainPage() {
    currentQuestionIndex.set(avatarCreationPageIndex + 1); // This will render the main page
  }
</script>

{#if $currentQuestionIndex === -1}
  <LoginScreen on:login={handleLogin} on:enter={handleCreateAccount}/>
{:else if $currentQuestionIndex >= 0 && $currentQuestionIndex < totalQuestions}
  {#if $currentQuestionIndex === 0}
    <PersonalityTestQ1 on:next={goToNextQuestion} on:previous={goToPreviousQuestion} />
  {:else if $currentQuestionIndex === 1}
    <PersonalityTestQ2 on:next={goToNextQuestion} on:previous={goToPreviousQuestion} />
  {:else if $currentQuestionIndex === 2}
    <PersonalityTestQ3 on:next={goToNextQuestion} on:previous={goToPreviousQuestion} />
  {:else if $currentQuestionIndex === 3}
    <PersonalityTestQ4 on:next={goToNextQuestion} on:previous={goToPreviousQuestion} />
  {/if}
{:else if $currentQuestionIndex === totalQuestions}
  <PersonalityTestQ5 on:finish={handleFinish} on:previous={goToPreviousQuestion} />
{:else if $currentQuestionIndex === avatarCreationPageIndex}
  <AvatarCreationPage on:finish={goToMainPage} />
{:else if $currentQuestionIndex === avatarCreationPageIndex + 1}
  <MainPage />
{/if}
