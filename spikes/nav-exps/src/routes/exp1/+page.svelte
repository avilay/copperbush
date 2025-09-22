<div class="card-container">
    <div class="card card-1">
        <h1>Card 1</h1>
        <p>This is the first card. Scroll down to see the next one!</p>
        <div class="card-menu">
            <a href="#profile-1">Profile-1</a>
            <a href="#comments-1">Comments-1</a>
            <a href="#like-1">Like-1</a>
        </div>
    </div>
    <div class="card card-2">
        <h1>Card 2</h1>
        <p>Welcome to the second card. Keep scrolling!</p>
        <div class="card-menu">
            <a href="#profile-2">Profile-2</a>
            <a href="#comments-2">Comments-2</a>
            <a href="#like-2">Like-2</a>
        </div>
    </div>
    <div class="card card-3">
        <h1>Card 3</h1>
        <p>You've reached the third card. Almost there!</p>
        <div class="card-menu">
            <a href="#profile-3">Profile-3</a>
            <a href="#comments-3">Comments-3</a>
            <a href="#like-3">Like-3</a>
        </div>
    </div>
    <div class="card card-4">
        <h1>Card 4</h1>
        <p>This is the fourth and final card. Thanks for viewing!</p>
        <div class="card-menu">
            <a href="#profile-4">Profile-4</a>
            <a href="#comments-4">Comments-4</a>
            <a href="#like-4">Like-4</a>
        </div>
    </div>
</div>

<style>
  .card-container {
    height: 100%;
    width: 100%;
  }

  .card {
      width: 100vw; /* Card width equals viewport width */
      height: 100vh; /* Card height equals viewport height */
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      font-family: Arial, sans-serif;
      color: white;
      font-size: 2em;
      box-sizing: border-box; /* Include padding and border in the element's total width and height */
      padding: 20px;
      text-align: center;

      position: relative; /* Make the card a positioning context for the menu */
      overflow: hidden; /* Ensure menu doesn't overflow if it somehow goes outside */
  }

  /* Example background colors for each card */
  .card-1 { background-color: #ff5733; }
  .card-2 { background-color: #33ff57; }
  .card-3 { background-color: #3357ff; }
  .card-4 { background-color: #ff33c1; }

  .card-menu {
      position: absolute; /* Position relative to the parent card */
      right: 20px; /* 20px from the right edge of the card */
      top: 50%; /* Center vertically */
      transform: translateY(-50%); /* Adjust for perfect vertical centering */
      display: flex;
      flex-direction: column; /* Stack links vertically */
      gap: 15px; /* Space between links */
      background-color: rgba(0, 0, 0, 0.5); /* Semi-transparent background */
      padding: 15px 10px;
      border-radius: 8px;
      z-index: 10; /* Ensure menu is on top of other card content */
  }

  .card-menu a {
      color: white;
      text-decoration: none;
      font-size: 0.7em; /* Smaller font size for menu links */
      white-space: nowrap; /* Prevent links from wrapping */
      padding: 5px;
      transition: background-color 0.3s ease;
  }

  .card-menu a:hover {
      background-color: rgba(255, 255, 255, 0.2);
      border-radius: 4px;
  }
</style>