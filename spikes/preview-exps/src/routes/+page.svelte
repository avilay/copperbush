<script lang="ts">
  import TopNav from "./TopNav.svelte";
  import BottomNav from "./BottomNav.svelte";
  import SideNav from "./SideNav.svelte";
  import Game from "./Game.svelte";
	import GameControl from "./GameControl.svelte";
  import { onMount, onDestroy } from "svelte";
  import playButton from "$lib/assets/play-button-pressed.png"

  const api = "http://192.168.29.171:8000";
  // const api = "http://localhost:8000";

  type PreloadedAsset = {
    videoUrl: string | null;
    posterUrl: string | null;
    isLoading: boolean;
    hasError: boolean;
  }

  type GameInfo = {
    id: string;
    name?: string;
    url: string;
    previewVideoUrl: string;
    previewPosterUrl: string;
    logoUrl: string;
    previewBackground: string;
    starCount: number;
    commentCount: number;
  };


  let previews: GameInfo[] = [
    {
      id: "game-1",
      name: "Lights",
      url: `${api}/lights`,
      previewVideoUrl: `${api}/lights/lights-preview.mp4`,
      previewPosterUrl: `${api}/lights/lights-preview.jpeg`,
      previewBackground: "dark",
      logoUrl: `${api}/lights/game-dev.png`,
      starCount: 1234,
      commentCount: 2
    },
    {
      id: "game-2",
      name: "Platformer",
      url: `${api}/platformer`,
      previewVideoUrl: `${api}/platformer/platformer-preview.mp4`,
      previewPosterUrl: `${api}/platformer/platformer-preview.jpeg`,
      previewBackground: "light",
      logoUrl: `${api}/platformer/game-dev.png`,
      starCount: 4,
      commentCount: 23000
    },
    {
      id: "game-3",
      name: "Space Invaders",
      url: `${api}/space-invaders`,
      previewVideoUrl: `${api}/space-invaders/space-invaders-preview.mp4`,
      previewPosterUrl: `${api}/space-invaders/space-invaders-preview.jpeg`,
      previewBackground: "dark",
      logoUrl: `${api}/space-invaders/game-dev.jpg`,
      starCount: 9459,
      commentCount: 2323
    },
    {
      id: "game-4",
      name: "Whack-A-Mole",
      url: `${api}/whack-a-mole`,
      previewVideoUrl: `${api}/whack-a-mole/whack-a-mole-preview.mp4`,
      previewPosterUrl: `${api}/whack-a-mole/whack-a-mole-preview.jpeg`,
      previewBackground: "dark",
      logoUrl: `${api}/whack-a-mole/game-dev.jpg`,
      starCount: 233,
      commentCount: 232343
    }
  ];

  let playGame: GameInfo | null = $state(null);
  let quitGameId: string | null = $state(null);

  // Preloading state management
  let preloadedAssets: Record<string, PreloadedAsset> = $state({});

  // Preloading functions
  async function preload(url: string): Promise<string | null> {
    // The reason for throwing within the try block and having a catch block is
    // that even though a 404 should not throw an error, the 404 triggers a 
    // CORS error that gets thrown. 
    try {
      const response = await fetch(url);
      if (!response.ok) {
        throw new Error(`Failed to fetch image: ${response.status}`);
      }
      const blob = await response.blob();
      return URL.createObjectURL(blob);
    } catch (error) {
      console.error(`Error preloading image ${url}:`, error);
      return null;
    }
  }

  async function preloadAll() {
    // Initialize loading states
    previews.forEach((preview) => {
      preloadedAssets[preview.id] = {
        videoUrl: null,
        posterUrl: null,
        isLoading: true,
        hasError: false
      }
    });

    // Start preloading all images
    const preloadPromises = previews.map(async (preview) => {
      const videoUrl = await preload(preview.previewVideoUrl);
      const posterUrl = await preload(preview.previewPosterUrl);
      preloadedAssets[preview.id] = {
        videoUrl: videoUrl,
        posterUrl: posterUrl,
        isLoading: false,
        hasError: videoUrl === null
      };
    });

    // Wait for all images to finish loading (success or failure)
    await Promise.allSettled(preloadPromises);
  }

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

  // Lifecycle hooks
  onMount(() => {
    console.log("onMount");
    preloadAll();

    return () => {
      console.log("Cleaning up all preloaded blobs");
      for (const imageState of Object.values(preloadedAssets)) {
        if (imageState.videoUrl) {
          URL.revokeObjectURL(imageState.videoUrl);
        }
        if (imageState.posterUrl) {
          URL.revokeObjectURL(imageState.posterUrl);
        }
      }  
    };
  });

  // $inspect(preloadedAssets).with(console.trace);
</script>

{#if playGame}
  <GameControl {onQuit} />
  <Game game={playGame}></Game>
  <div>Playing game</div>
{:else}
  <TopNav />
  <div id="previews">
    {#each previews as game}
      {@const preloadedState = preloadedAssets[game.id]}
      {@const isLoading = preloadedState?.isLoading ?? true}
      {@const hasError = preloadedState?.hasError ?? false}

      <div class="preview" id="{game.id}">
        {#if isLoading}
          <div class="loading-placeholder">
            <p>Loading preview...</p>
            <div class="loading-spinner"></div>
          </div>
        {:else if hasError}
          <div class="error-placeholder">
            <p>Failed to load preview</p>
          </div>
        {:else}
          <video autoplay loop muted playsinline preload="auto" poster="{preloadedAssets[game.id].videoUrl}">
            <source src="{preloadedAssets[game.id].videoUrl}" type="video/mp4">
          </video>
        {/if}

        <button class="play-btn" onclick={onPlay}>
          <img src="{playButton}" alt="play button" />
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

  video {
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

  .loading-placeholder,
  .error-placeholder {
    width: 100%;
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
    background-color: #2a2a2a;
    color: white;
  }

  .loading-spinner {
    width: 40px;
    height: 40px;
    border: 4px solid #333;
    border-top: 4px solid #fff;
    border-radius: 50%;
    animation: spin 1s linear infinite;
    margin-bottom: 16px;
  }

  @keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
  }

  .loading-placeholder p,
  .error-placeholder p {
    margin: 5em;
    text-align: center;
  }

  .error-placeholder {
    background-color: #ba3434;
  }
</style>
