<script lang="ts">
  import TopNav from "../TopNav.svelte";
  import BottomNav from "../BottomNav.svelte";
  import starIconOutline from "$lib/assets/star-icon-outline.svg";
  import commentIconOutline from "$lib/assets/comment-icon-outline.svg";
  import friendAddIconOutline from "$lib/assets/friend-add-icon-outline.svg";

  // const api = "http://192.168.5.140:8000";
  const api = "http://localhost:8000";

  let previews: Game[] = [
    {
      id: "game-1",
      name: "Lights",
      url: `${api}/lights`,
      previewCardUrl: `${api}/lights/lights-preview.jpeg`,
      previewBackground: "dark",
      logoUrl: `${api}/lights/game-dev.png`,
      starCount: 1234,
      commentCount: 2
    },
    {
      id: "game-2",
      name: "Platformer",
      url: `${api}/platformer`,
      previewCardUrl: `${api}/platformer/platformer-preview.jpeg`,
      previewBackground: "light",
      logoUrl: `${api}/platformer/game-dev.png`,
      starCount: 4,
      commentCount: 23000
    },
    {
      id: "game-3",
      name: "Space Invaders",
      url: `${api}/space-invaders`,
      previewCardUrl: `${api}/space-invaders/space-invaders-preview.jpeg`,
      previewBackground: "dark",
      logoUrl: `${api}/space-invaders/game-dev.jpg`,
      starCount: 9459,
      commentCount: 2323
    },
    {
      id: "game-4",
      name: "Whack-A-Mole",
      url: `${api}/whack-a-mole`,
      previewCardUrl: `${api}/whack-a-mole/whack-a-mole-preview.jpeg`,
      previewBackground: "dark",
      logoUrl: `${api}/whack-a-mole/game-dev.jpg`,
      starCount: 233,
      commentCount: 232343
    }
  ];
</script>

<TopNav />
<div id="previews">
{#each previews as game}
  {@const color = game.previewBackground === 'dark' ? '#fff' : '#000'}
  <div class="preview" id="{game.id}">
    <img src="{game.previewCardUrl}" alt="game preview gif" />
    <nav>
      <ul>
        <li class="menu-item">
          <a href="/dev">
            <img class="profile" src="{game.logoUrl}" alt="logo of game developer" />
          </a>
        </li>
        <li class="menu-item">
          <a href="/star" style="color: {color}">
            <div>
              <img class="icon" src="{starIconOutline}" alt="star icon" />
              {game.starCount}
            </div>
          </a>
        </li>
        <li class="menu-item">
          <a href="/comments" style="color: {color}">
            <div>
              <img class="icon" src="{commentIconOutline}" alt="comment icon" />
              {game.commentCount}
            </div>
          </a>
        </li>
        <li class="menu-item">
          <a href="/invite">
            <div><img class="icon" src="{friendAddIconOutline}" alt="invite friend icon" /></div>
          </a>
        </li>
      </ul>
    </nav>
  </div>
{/each}
</div> 
<BottomNav />

<style>
  #previews {
    background-color: lightpink;
    padding: 0;
    overflow-y: scroll;
    height: 100vh;
    scroll-snap-type: y mandatory; /* Enable scroll snapping */
    -webkit-overflow-scrolling: touch; /* Smooth scrolling on iOS */
  }

  .preview {
    height: 100vh;
    position: relative;
    overflow: hidden;
    scroll-snap-align: start; /* Snap to the start of each card */
  }

  img {
    width: 100%;
    height: 100vh;
    object-fit: cover;
  }

  nav {
    background-color: transparent;
    position: absolute;
    right: 5px;
    top: 50%;
    transform: translateY(-50%);
    z-index: 10;
  }

  nav > ul {
    display: flex;
    flex-flow: column nowrap;
    justify-content: flex-start;
    align-items: center;
    gap: 2em;
    padding: 0;
    margin: 0.25em;
    font-size: 0.75rem;
  }

  .menu-item {
    list-style-type: none;
  }

  .menu-item > a {
    padding: 0;
    margin: 0;
    font-family: inherit;
    text-decoration: none;
    text-align: center;
  }

  .profile {
    width: 64px;
    height: 64px;
    border-radius: 50%; /* Makes the image circular */
    object-fit: cover; /* Ensures the image covers the area without distortion */
  }

  .icon {
    width: 32px;
    height: 32px;
    display: block;
  }
</style>