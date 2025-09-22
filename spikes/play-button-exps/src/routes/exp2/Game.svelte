<script lang="ts">
  let { game, onQuit } = $props();
  console.log(game.id);
  console.log(game.url);

  let isQuitting = $state(false);

  function onQuitClicked(e: MouseEvent) {
    e.preventDefault();
    isQuitting = true;
    // Doing this on a delay to give the browser time to clean up the iframe
    // and show the user a disabled quit button.
    setTimeout(() => {onQuit()}, 100);
  }

</script>

<div>
  {#if isQuitting}
    <button onclick={onQuitClicked} disabled>Quitting...</button>
  {:else}
    <button onclick={onQuitClicked}>Quit</button>
  {/if}
  <iframe 
    src="{game.url}" 
    title="MelonJS {game.id} Example"
    width="100%" 
    height="600px"
    frameborder="0">
  </iframe>
</div>

<style>
  iframe {
    border: none;
    min-height: 100vh;
  }
</style>