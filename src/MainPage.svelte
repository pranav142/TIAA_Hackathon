<script>
  import {onMount} from 'svelte';
  let streak = 5; // Your streak count
  let leaderboard = [ // This is your sample leaderboard data
    { id: 1, name: 'Alice', score: 3000 },
    { id: 2, name: 'Bob', score: 2500 },
    { id: 3, name: 'Charlie', score: 2000 },
    { id: 4, name: 'Diana', score: 1500 },
    { id: 5, name: 'Evan', score: 1000 },
  ];

    onMount(() => {
    const script = document.createElement('script');
    script.type = 'module';
    script.src = 'https://unpkg.com/@google/model-viewer/dist/model-viewer.min.js';
    document.body.appendChild(script);
  });

</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Kenia&display=swap');
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.1.1/css/all.min.css');

.main-page {
  display: grid;
  grid-template-columns: 200px 1fr; /* Adjust the 200px to the width of your sidebar */
  grid-template-rows: auto;
  grid-template-areas: "sidebar left";
  height: 100vh;
  color: white;
  background-color: linear-gradient(to top, rgb(20, 2, 2), rgb(105, 23, 23));
  font-family: Arial, sans-serif;
}

  .fire-icon {
    transition: transform 0.3s ease;
  }



.topbar {
  background: rgb(0,0,0);
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 70px;
  padding: 0 20px;
  z-index: 1000;
  display: flex;
  align-items: center;
    font-size: 30px; /* Larger font size, adjust as needed */
  font-family: 'Kenia', sans-serif;
  font-style: italic;
  font-weight: bold;
  color: #ffffff;
}

.topbar-left {
  flex: 1;
  text-align: left; /* Aligns the text to the left */
  padding-left:68px;
  color:red;
}

.topbar-center {
  flex: 2;
  text-align: center; /* Aligns the text to the center */
  font-style: normal;
  font-size:25px;
}

.topbar-right {
  flex: 1;
  text-align: right; /* Aligns the text to the right */
}

  .sidebar {

    background: rgb(0,0,0);
    position: fixed;
    top: 51px;
    left: 0;
    width: 300px;
    height: 100%;
    padding: 20px 0;
    transition: all 0.5s ease;
    font-size: 25px;
    font-weight: bold;
    display: flex;
      flex-direction: column;
  }

  .sidebar-top{
    flex-grow:1;
    padding: 40px;
    padding-left:50px;
    white-space: nowrap;
    text-overflow: ellipses;
  }

  .challenge {
    margin-top: 20px;
    font-size: 18px; /* Adjust the font size as necessary */
    overflow-wrap: break-word;
    white-space:wrap;
    /* Add any additional styling as required */
}

 .sidebar-bottom {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-top: auto;
  padding-bottom: 120px; /* Padding on all sides */
  padding-left:70px;
 /* Reduced extra padding at the bottom */
  gap: 30px; /* This will ensure there is a 30px gap between child elements */
}

.sidebar-bottom:hover {
    cursor: pointer;
}
  
  .right-sidebar {
      background: linear-gradient(to right, rgb(0,0,0), rgb(41,4,4));
  position: fixed;
  top: 51px;
  right: 0; /* This positions the sidebar on the right */
  width: 300px;
  height: 100%;
  padding: 20px 0;
  transition: all 0.5s ease;
  }




  .logo {
    font-size: 32px; /* Large font size for logo */
    font-weight: bold;
    margin-bottom: 50px; /* Space from the top */
  }

  .menu-item {
    margin: 10px 0;
    font-size: 20px;
    /* Add additional styling for menu items */
  }

  .streak-container {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    margin: 20px 0;
    text-align: center;
    position: fixed;
    bottom: 30px;
    left:700px;
  }

  .streak-number {
    font-size: 3em; /* Very large font size for streak number */
    margin-right: 0.5em; /* Spacing between number and icon */
  }

  .fire-icon {
    transition: transform 0.3s ease;
  }

  .main {
    grid-area: main;
    background-color: #1D3557; /* Assuming a dark theme from your image */
    padding: 20px; /* Adjust padding as needed */
    display: flex;
    justify-content: space-around;
    align-items: center;
    flex-direction: column;
  }

  #modelviewer {
    height: 400px;
    width: 100%;
    max-width: 600px;
    margin: 0 auto; 
    position: fixed;
    top:200px;
    left:450px;/* Center the model viewer */
  }

  .avatar-container {
    /* Container for the avatar */
    max-width: 200px; /* Adjust based on your image size */
    margin-bottom: 20px;
  }

  .avatar-image {
    width: 100%;
    height: auto;
  }
  .leaderboard {
    /* Styles for the leaderboard */
    background: #6D6875; /* Darker background for the leaderboard */
    padding: 20px;
    border-radius: 10px; /* Rounded corners */
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); /* Shadow for depth */
    width: 80%; /* Adjust as needed */
    margin-bottom: 20px;
  }


  .title {
    font-size: 24px; /* Font size for leaderboard title */
    margin-bottom: 10px;
  }

.leaderboard {
  position: absolute;
  top:10px;
  right:10px;
  height: 315px;
  width: 100%; /* Ensure the container spans the full width */
  background: #E63946; /* Red background */
  border-radius: 15px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); /* Add some shadow for depth */
  color: white;
  max-width: 400px; /* Adjust as needed */
  margin: auto;
  overflow: hidden; /* Ensures the child elements do not overflow the rounded corners */
}


.title {
  background: #F1FAEE; /* Light background for the title */
  color: #1D3557; /* Dark color for the title text */
  text-transform: uppercase; /* Capitalize the title */
  font-size: 1.5em; /* Larger font size */
  padding: 0.5em 0; /* Add padding on the top and bottom */
  text-align: center;
  margin: 0; /* Reset any default margins */
  font-weight: bold; /* Make the title bold */
}

.entry {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1em; /* Increase padding */
  border-bottom: 1px solid #6D6875; /* Add a separator between entries */
  transition: background-color 0.3s ease; /* Transition for hover effect */
}

.entry:last-child {
  border-bottom: none; /* No border for the last item */
}

.entry:hover {
  background-color: #6D6875; /* Lighter background on hover */
}

.rank {
  display: flex;
  align-items: center;
}

/* Adjust .rank img size and margins if necessary */
.rank img {
  width: 24px; /* Adjust as necessary */
  height: 24px; /* Adjust as necessary */
  margin-right: 0.5em;
}

.name {
  flex-grow: 1; /* Ensures the name takes up available space */
  margin-left: 1em; /* Space out the rank icon and the name */
}

.score {
  font-weight: bold; /* Make the score bold */
}

#modelviewer {
    height: 400px;
    width: 100%; /* Make it responsive */
    max-width: 600px; /* Max width to control the size on larger screens */
  }

/* You might need additional styles for fonts, spacings, or to import icons */


  /* Additional styles for your leaderboard and other components would go here */
</style>

<div class="main-page">
    <div class="streak-container">
    <div class="streak-number">{streak}</div>
    <div class="fire-icon" style="transform: scale({1 + streak / 100});">
        <!-- Replace with your own fire icon PNG file -->
        <img src="/Fire no background.gif" alt="Fire Icon" /> <!-- Make sure the path is correct -->
    </div>
    </div>

     <model-viewer
      id="modelviewer"
      alt="Ready Player Me Avatar"
      src="https://models.readyplayer.me/6546fdc2444d953355fdbcae.glb"
      shadow-intensity="1"
      camera-controls
      touch-action="pan-y"
    ></model-viewer>

    
<div class="sidebar">
    <!-- Sidebar content goes here -->
    <div class="sidebar-top">
        <div>Daily Challenge</div>
        <div class="challenge">Spend $5 on a fancy dessert or add it to your travel fund?</div>
    </div>
    <div class="sidebar-bottom">
        <div><i class="fas fa-cog" style="color: red"></i> Settings</div>
        <div><i class="fas fa-sign-out-alt" style="color: red"></i> Log Out</div>
    </div>
</div>

  

<div class="topbar">
  <div class="topbar-left">
    Investify <!-- This is your left-aligned text -->
  </div>
  <div class="topbar-center">
    Words of Encouragement <!-- This is your center-aligned text -->
  </div>
  <div class="topbar-right">
    <!-- Right-aligned text or elements can go here if needed -->
  </div>
</div>


  <!-- This is where your leaderboard would be rendered -->
   <div class="right-sidebar">
  <div class="title">LEADERBOARD</div>
  {#each leaderboard as player (player.id)}
    <div class="entry">
      <div class="rank">{player.id}</div>
      <div class="name">{player.name}</div>
      <div class="score">{player.score}</div>
    </div>
  {/each}
</div>
  
  <!-- The rest of your main page content goes here -->
</div>
