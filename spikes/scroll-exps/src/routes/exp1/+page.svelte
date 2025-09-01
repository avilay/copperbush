<script lang="ts">
  let clientX = $state(0.0);
  let clientY = $state(0.0);

  let pageX = $state(0.0);
  let pageY = $state(0.0);
  
  let screenX = $state(0.0);
  let screenY = $state(0.0);

  let pointerState = $state("");
  let msg = $state("");

  const sensitivity = 10;

  function onPointerUp(e: Event) {
    const pe = e as PointerEvent;

    let diffX = pe.clientX - clientX;
    let diffY = pe.clientY - clientY;

    msg = "";

    // If both dx and dy have crossed the sensitivty threshold, then the one
    // with the greater magnitude determines the direction.
    if (Math.abs(diffX) > sensitivity && Math.abs(diffY) > sensitivity) {
      if (Math.abs(diffX) > Math.abs(diffY)) {
        // Horizontal swipe
        if (diffX < 0) {
          msg = "You swiped left";
        } else {
          msg = "You swiped right";
        }
      } else {
        // Vertical swipe
        if (diffY < 0) {
          msg = "You swiped up";
        } else {
          msg = "You swiped down";
        }
      }
    // Otherwise, the one that has crossed the sensitivity threshold determines
    // the direction.
    } else if (Math.abs(diffX) > sensitivity && Math.abs(diffY) < sensitivity) {
      // Horizontal swipe
        if (diffX < 0) {
          msg = "You swiped left";
        } else {
          msg = "You swiped right";
        }
    } else if (Math.abs(diffX) < sensitivity && Math.abs(diffY) > sensitivity) {
      // Vertical swipe
        if (diffY < 0) {
          msg = "You swiped up";
        } else {
          msg = "You swiped down";
        }
    } else {
      // Both the x and y directions are below the sensitivity threshold.
      msg = "You did not swipe";
    }

    msg += ` dX = ${diffX.toFixed(2)}, dY = ${diffY.toFixed(2)}`;

    clientX = pe.clientX;
    clientY = pe.clientY;

    pageX = pe.pageX;
    pageY = pe.pageY;

    screenX = pe.screenX;
    screenY = pe.screenY;

    pointerState = "pointerup";

    e.currentTarget?.removeEventListener("pointerup", onPointerUp);
  }

  function onPointerDown(e: PointerEvent) {
    clientX = e.clientX;
    clientY = e.clientY;

    pageX = e.pageX;
    pageY = e.pageY;

    screenX = e.screenX;
    screenY = e.screenY;

    pointerState = "pointerdown";

    e.currentTarget?.addEventListener("pointerup", onPointerUp);
  }
  
</script>

<div id="preview" onpointerdown={onPointerDown}>
  <p>{msg}</p>
  <p>Pointer state: {pointerState}</p>
  Contact coordinates:
  <ul>
    <li>Client: ({clientX.toFixed(2)}, {clientY.toFixed(2)})</li>
    <li>Page: ({pageX.toFixed(2)}, {pageY.toFixed(2)})</li>
    <li>Screen: ({screenX.toFixed(2)}, {screenY.toFixed(2)})</li>
  </ul>
</div>

<style>
  #preview {
    padding: 1rem;
    height: 92vh;
    background-color: lightblue;
    touch-action: none;
  }
</style>