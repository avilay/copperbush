<script lang="ts">
  let prevY = $state(0.0);
  let idx = $state(0);

  let previews = ["placeholder-0", "placeholder-1", "placeholder-2", "placeholder-3", "placeholder-4", "placeholder-5"];

  const sensitivity = 10;

  function onPointerMove(e: Event) {
    console.log("onPointerMove");
    const pe = e as PointerEvent;
    
    let diffY = Math.round(pe.clientY - prevY);
    prevY = pe.clientY;
    const previews = document.getElementById("previews")!;
    console.debug(`diffY: ${diffY}, scrolling by: ${-50 * diffY}`);
    previews.scrollBy({top: -50 * diffY, left: 0, behavior: "smooth"});
  }

  function onPointerDown(e: PointerEvent) {
    console.log("onPointerDown");
    prevY = e.clientY;
    // e.currentTarget?.addEventListener("pointerup", onPointerUp);
  }
  
</script>

<div id="previews" onpointerdown={onPointerDown} onpointermove={onPointerMove}>
  <div id="preview-0">
    <img src="placeholder-0.png" alt="platformer game preview" />
  </div>
  <div id="preview-1">
    <img src="placeholder-1.png" alt="spotlight game preview" />
  </div>
</div> 

<style>
  #previews {
    background-color: lightpink;
    padding: 0;
    overflow-y: hidden;
    /* overflow: auto; */
    height: 100vh;
    touch-action: none;
  }

  img {
    width: 100%;
    height: 100vh;
    object-fit: cover;
  }
</style>