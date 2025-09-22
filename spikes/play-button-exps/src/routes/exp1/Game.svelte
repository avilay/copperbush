<script lang="ts">
  let { game } = $props();
  console.log(game.id);
  console.log(game.url);

</script>

<div>
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