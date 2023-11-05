<script>
  let streak = 5; // Your streak count
  let leaderboard = []; // This would be populated with leaderboard data
</script>

<style>
  /* Add additional styles as needed */
  .streak-container {
    position: absolute;
    top: 10px;
    left: 10px;
    display: flex;
    align-items: center;
  }

  .streak-number {
    font-size: 2em; /* Large font size for streak number */
    margin-right: 0.5em; /* Spacing between number and icon */
  }

  .fire-icon {
    transition: transform 0.3s ease;
  }

  .leaderboard {
    position: absolute;
    top: 10px;
    right: 10px;
  }

  /* Additional styles for your leaderboard and other components would go here */
</style>

<div class="main-page">
  <div class="streak-container">
    <div class="streak-number">{streak}</div>
    <div class="fire-icon" style="transform: scale({1 + streak / 100});">
      <!-- Replace with your own fire icon SVG file -->
     <img src="/Users/sameerbhagavatula/Documents/Documents/VS CODE/Python/svelte-login/src/icons8-fire.gif" alt="Fire Icon" />
      <!-- Make sure the path is correct -->
    </div>
  </div>
  
  <!-- This is where your leaderboard would be rendered -->
  <div class="leaderboard">
    <h2>Leaderboard</h2>
    <!-- You'll probably want to render this list based on some dynamic data -->
    <ol>
      <li>User A - 120 points</li>
      <li>User B - 110 points</li>
      <li>User C - 100 points</li>
      <!-- ... -->
    </ol>
  </div>
  
  <!-- The rest of your main page content goes here -->
</div>
