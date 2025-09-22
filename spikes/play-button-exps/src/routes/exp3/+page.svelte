<script lang="ts">
  import { fade } from "svelte/transition";
  import TopNav from "../TopNav.svelte";
  import BottomNav from "../BottomNav.svelte";
  import SideNav from "../SideNav.svelte";
  import Game from "./Game.svelte";
	import GameControl from "./GameControl.svelte";

  import lightsPreviewImg from "$lib/assets/lights-preview.jpeg";
  import platformerPreviewImg from "$lib/assets/platformer-preview.jpeg";
  import spaceInvadersPreviewImg from "$lib/assets/space-invaders-preview.jpeg";
  import whackAMolePreviewImg from "$lib/assets/whack-a-mole-preview.jpeg";

  const api = "http://192.168.29.171:8000";
  // const api = "http://localhost:8000";

  let previews: GameInfo[] = [
    {
      id: "game-1",
      name: "Lights",
      url: `${api}/lights`,
      previewCardUrl: lightsPreviewImg,
      previewBackground: "dark",
      logoUrl: `${api}/lights/game-dev.png`,
      starCount: 1234,
      commentCount: 2
    },
    {
      id: "game-2",
      name: "Platformer",
      url: `${api}/platformer`,
      previewCardUrl: platformerPreviewImg,
      previewBackground: "light",
      logoUrl: `${api}/platformer/game-dev.png`,
      starCount: 4,
      commentCount: 23000
    },
    {
      id: "game-3",
      name: "Space Invaders",
      url: `${api}/space-invaders`,
      previewCardUrl: spaceInvadersPreviewImg,
      previewBackground: "dark",
      logoUrl: `${api}/space-invaders/game-dev.jpg`,
      starCount: 9459,
      commentCount: 2323
    },
    {
      id: "game-4",
      name: "Whack-A-Mole",
      url: `${api}/whack-a-mole`,
      previewCardUrl: whackAMolePreviewImg,
      previewBackground: "dark",
      logoUrl: `${api}/whack-a-mole/game-dev.jpg`,
      starCount: 233,
      commentCount: 232343
    }
  ];

  let playGame: GameInfo | null = $state(null);
  let quitGameId: string | null = $state(null);

  function onPlay(e: MouseEvent) {
    // Get the preview div - e.target is the img element, so I need to get its
    // grandparent.
    const previewDiv = (e.target as HTMLElement).parentElement!.parentElement!;
    const gameId = previewDiv.id;
    playGame = previews.filter((p: GameInfo) => p.id === gameId)[0];
  }

  function onQuit() {
    console.log("Game was quit");
    if (playGame) {
      quitGameId = playGame.id;
      playGame = null;
    }
  }

  $effect(() => {
    if (quitGameId) {
      const previewDiv = document.getElementById(quitGameId)!;
      previewDiv.scrollIntoView({behavior: "instant"});
    }
  });

</script>

{#if playGame}
  <GameControl {onQuit} />
  <Game game={playGame}></Game>
  <div>Playing game</div>
{:else}
  <TopNav />
  <div id="previews">
    {#each previews as game}
      <div class="preview" id="{game.id}">
        <img src="{game.previewCardUrl}" alt="game preview gif" />
        <button transition:fade class="play-btn" onclick={onPlay}>
          <img src="/play-button-pressed.png" alt="play button" />
        </button>
        <SideNav {game} />
      </div>
    {/each}
  </div> 
  <BottomNav />
{/if}

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

  .play-btn {
    background: transparent;
    position: absolute;
    border: 0;
    margin: 0;
    top: 50%;
    left: 50%;
    transform: translateX(-50%) translateY(-50%);
    z-index: 5; /* Ensure it's above other content if needed, but below the menu */
  }

  .play-btn > img {
    height: 100%;
    width: 100%;
    object-fit: cover;
  }
</style>