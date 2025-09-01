<script lang="ts">
  import Game from "../Game.svelte";
  import TopNav from "../TopNav.svelte";

  let showGame = $state(false);

  function onClick() {
    showGame = true;
  }

  function onQuit() {
    showGame = false;
  }
</script>

{#if showGame}
<Game game={{id: "platformer", url: "http://localhost:8000/platformer"}} {onQuit}></Game>
{:else}
<TopNav />
<div class="container">
  <h1>Game Feed</h1>
  <button onclick={onClick}>Play!</button>
</div>
{/if}

<style>
  .container {
    width: 90%;
    margin: 4em auto 0 auto;
    text-align: center;
  }
</style>