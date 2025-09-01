<script lang="ts">
  let previews = ["platformer", "spotlight", "sprites", "placeholder-1", "placeholder2", "placeholder-3"];

  function onScrollEnd(e: Event) {
    console.log("Entering onScrollEnd");
    // Remove event listener so that any scrolling that happens in this function
    // does not trigger another scrollend event
    e.currentTarget!.removeEventListener("scrollend", onScrollEnd);

    const previewDiv = document.getElementById("preview")!;

    // Ensure that a preview has scrolled completely to the top
    // console.log("Scrolling view to the top");
    const currPreview = Array.from(previewDiv.children).find((child) => child.getBoundingClientRect().top >= 0)! as HTMLElement;
    // currPreview.scrollIntoView({ behavior: "smooth" });

    const currIdx = parseInt(currPreview.id.split("-")[1]);

    // Ensure that there is preview after this, if not, load it.
    if (currIdx < previews.length - 1) {
      if (!currPreview.nextSibling) {
        console.log("Adding a new node at the end");
        // Add a new node at the end
        const newPreview = currPreview.cloneNode(true) as HTMLElement;
        newPreview.id = `preview-${currIdx + 1}`;
        newPreview.getElementsByTagName("img")[0].src = `${previews[(currIdx + 1)]}.png`;
        previewDiv.appendChild(newPreview);

        // Get rid of the first node
        if (previewDiv.children.length > 3) {
          console.log("Removing the first node");
          previewDiv.removeChild(previewDiv.children[0]);
        }
      }
    }  // else this is the last preview, there aren't supposed to be any after this.

    // Ensure that there is a preview before this, if not, load it.
    if (currIdx > 0) {
      if (!currPreview.previousSibling) {
        // Add a new node at the beginning
        console.log("Adding a new node at the beginning");
        const newPreview = document.createElement("div");
        newPreview.id = `preview-${currIdx - 1}`;
        newPreview.innerHTML = `<img src="${previews[(currIdx - 1)]}.png" alt="${previews[(currIdx - 1)]} game preview" />`;
        previewDiv.insertBefore(newPreview, currPreview);

        // Get rid of the last node
        if (previewDiv.children.length > 3) {
          console.log("Removing the last node");
          previewDiv.removeChild(previewDiv.children[previewDiv.children.length - 1]);
        }
      }
    }  // else this is the first preview, there aren't supposed to be any before this.

    // Add the event listener back
    // e.currentTarget!.addEventListener("scrollend", onScrollEnd);
    console.log("Leaving onScrollEnd");
  }
</script>

<div id="preview" onscrollend={onScrollEnd}>
  <div id="preview-0"><img src="platformer.png" alt="platformer game preview" /></div>
  <div id="preview-1"><img src="spotlight.png" alt="spotlight game preview" /></div>
</div> 

<style>
  #preview {
    background-color: lightblue;
    padding: 0;
    /* overflow-y: auto; */
    overflow: scroll;
    height: 100vh;
  }

  img {
    width: 100%;
    height: 100vh;
    object-fit: cover;
  }
</style>