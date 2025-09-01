<script lang="ts">
  let previews = ["placeholder-0", "placeholder-1", "placeholder-2", "placeholder-3", "placeholder-4", "placeholder-5"];
  let timeoutHandle = $state(0);

  function refreshPreviews(visiblePreview: HTMLElement) {
    const currIdx = parseInt(visiblePreview.id.split("-")[1]);
    const previewsDiv = document.getElementById("preview")!;
    if (currIdx === 0) {
      while (previewsDiv.children.length > 2) {
        previewsDiv.removeChild(previewsDiv.lastElementChild!);
      }
    } else if (currIdx === previews.length - 1) {
      while (previewsDiv.children.length > 2) {
        previewsDiv.removeChild(previewsDiv.firstElementChild!);
      }
    } else if (currIdx > 0 && currIdx < previews.length - 1) {
      if (!visiblePreview.nextElementSibling) {
        const newPreview = visiblePreview.cloneNode(true) as HTMLElement;
        newPreview.id = `preview-${currIdx + 1}`;
        newPreview.getElementsByTagName("img")[0].src = `${previews[(currIdx + 1)]}.png`;
        console.debug(`Adding ${newPreview.id}`);
        previewsDiv.appendChild(newPreview);

        while (previewsDiv.children.length > 3) {
          console.debug(`Removing ${previewsDiv.firstElementChild?.id}`)
          previewsDiv.removeChild(previewsDiv.firstElementChild!);
        }
      }

      if (!visiblePreview.previousElementSibling) {
        const newPreview = visiblePreview.cloneNode(true) as HTMLElement;
        newPreview.id = `preview-${currIdx - 1}`;
        newPreview.getElementsByTagName("img")[0].src = `${previews[(currIdx - 1)]}.png`;
        console.debug(`Adding ${newPreview.id}`);
        previewsDiv.insertBefore(newPreview, visiblePreview);

        while (previewsDiv.children.length > 3) {
          console.debug(`Removing ${previewsDiv.lastElementChild?.id}`);
          previewsDiv.removeChild(previewsDiv.lastElementChild!);
        }
      }
    } else {
      console.error("KA-BOOM!!");
    }

    if (!isOnTop(visiblePreview.getBoundingClientRect().top)) {
      console.debug(`Appearing ${visiblePreview.id} into view`);
      visiblePreview.scrollIntoView();
    }
  }

  function isOnTop(y: number): boolean {
    return Math.abs(y) < 5;
  }

  function onScrollEnd() {
    console.debug(`(${new Date().valueOf()}) - onScrollEnd`);
    const previewsDiv = document.getElementById("preview")!;

    // Complete the scroll of any partially scrolled preview
    // TODO: Explore if Intersection Observer API will be a better way
    let visiblePreview: HTMLElement;
    let element = Array.from(previewsDiv.children).find((child) => child.getBoundingClientRect().top >= 0);
    if (!element) {
      // If the last element is visible, then the top scrolls to -4
      visiblePreview = previewsDiv.lastElementChild! as HTMLElement;
    } else {
      if (element.getBoundingClientRect().top < window.innerHeight/2) {
        // This element is near the top, make this visible
        visiblePreview = element as HTMLElement;
      } else {
        // This element is closer to the bottom, make the previous element visible
        visiblePreview = element.previousElementSibling! as HTMLElement;
      }
    }

    const top = Math.round(visiblePreview.getBoundingClientRect().top);
    if (!isOnTop(top)) {
      console.debug(`Scrolling ${visiblePreview.id} into view`);
      visiblePreview.scrollIntoView({behavior: "smooth"});
    }

    if (isOnTop(top)) {
      refreshPreviews(visiblePreview);
    } else {
      console.debug(`Top is not zero: ${top} (${new Date().valueOf()})`);
    }

    
  }

  function onScroll(e: Event) {
    // Reset the timeout handle everytime scrolling occurs.
    // Eventually when the timeout function is called it is safe to assume that
    // scrolling has stopped.
    clearTimeout(timeoutHandle);
    timeoutHandle = setTimeout(onScrollEnd, 3000);
  }
  
</script>
<div id="preview" onscroll={onScroll}>
  <div id="preview-0">
    <img src="placeholder-0.png" alt="platformer game preview" />
  </div>
  <div id="preview-1">
    <img src="placeholder-1.png" alt="spotlight game preview" />
  </div>
</div> 

<style>
  #preview {
    background-color: lightpink;
    padding: 0;
    overflow-y: auto;
    /* overflow: auto; */
    height: 100vh;
    overscroll-behavior: none;
  }

  img {
    width: 100%;
    height: 100vh;
    object-fit: cover;
  }
</style>