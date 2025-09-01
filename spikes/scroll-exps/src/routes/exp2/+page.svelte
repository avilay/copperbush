<script lang="ts">
  let clientY = $state(0.0);
  let idx = $state(0);

  let previews = ["platformer", "spotlight", "sprites"];

  const sensitivity = 10;

  function onSwipeUp() {
    console.log("Swiped Up");
    idx = (idx + 1) % previews.length;
  }

  function onSwipeDown() {
    console.log("Swiped Down");
    if (idx > 0) {
      idx = (idx - 1) % previews.length;
    }
  }

  function onPointerUp(e: Event) {
    console.log("onPointerUp");
    e.currentTarget?.removeEventListener("pointerup", onPointerUp);
    const pe = e as PointerEvent;

    let diffY = pe.clientY - clientY;
    clientY = pe.clientY;

    if (Math.abs(diffY) > sensitivity) {
      console.log("Swiped");
      diffY < 0 ? onSwipeUp() : onSwipeDown();
    }    
  }

  function onPointerDown(e: PointerEvent) {
    console.log("onPointerDown");
    clientY = e.clientY;
    e.currentTarget?.addEventListener("pointerup", onPointerUp);
  }
  
</script>

<div id="preview" onpointerdown={onPointerDown}>
  <img src="{previews[idx]}.png" alt="{previews[idx]} game preview" />
</div> 

<style>
  #preview {
    background-color: lightblue;
    padding: 0;
    touch-action: none;
  }

  img {
    width: 100%;
    height: 100vh;
    object-fit: cover;
  }
</style>