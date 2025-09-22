<script lang="ts">
  import TopNav from "../TopNav.svelte";
  import BottomNav from "../BottomNav.svelte";
  import SideNav from "./SideNav.svelte";

  const api = "http://192.168.5.140:8000";
  // const api = "http://localhost:8000";

  let previews: Game[] = [
    {
      id: "game-1",
      name: "Lights",
      url: `${api}/lights`,
      previewCardUrl: `${api}/lights/lights-preview-dim.gif`,
      previewBackground: "dark",
      logoUrl: `${api}/lights/game-dev.png`,
      starCount: 1234,
      commentCount: 2
    },
    {
      id: "game-2",
      name: "Platformer",
      url: `${api}/platformer`,
      previewCardUrl: `${api}/platformer/platformer-preview-dim.gif`,
      previewBackground: "light",
      logoUrl: `${api}/platformer/game-dev.png`,
      starCount: 4,
      commentCount: 23000
    },
    {
      id: "game-3",
      name: "Space Invaders",
      url: `${api}/space-invaders`,
      previewCardUrl: `${api}/space-invaders/space-invaders-preview-dim.gif`,
      previewBackground: "dark",
      logoUrl: `${api}/space-invaders/game-dev.jpg`,
      starCount: 9459,
      commentCount: 2323
    },
    {
      id: "game-4",
      name: "Whack-A-Mole",
      url: `${api}/whack-a-mole`,
      previewCardUrl: `${api}/whack-a-mole/whack-a-mole-preview-dim.gif`,
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
  <div class="preview" id="{game.id}">
    <img src="{game.previewCardUrl}" alt="game preview gif" />
    <SideNav {game} />
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
</style>