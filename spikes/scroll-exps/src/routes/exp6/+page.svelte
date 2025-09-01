<script lang="ts">
  let previews = ["placeholder-0", "placeholder-1", "placeholder-2", "placeholder-3", "placeholder-4", "placeholder-5"];
</script>

<div id="previews">
{#each previews as preview, idx}
  <div class="preview" id="preview-{idx}">
    <img src="/{preview}.png" alt="game preview gif" />
  </div>
{/each}
</div> 

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
    scroll-snap-align: start; /* Snap to the start of each card */
  }

  img {
    width: 100%;
    height: 100vh;
    object-fit: cover;
  }
</style>