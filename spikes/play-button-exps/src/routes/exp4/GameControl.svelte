<script lang="ts">
  import closeIcon from "$lib/assets/close-icon.svg";

  let { onQuit } = $props();
</script>

<nav>
  <ul>
    <li>
      <button onclick={onQuit}>
        <img src="{closeIcon}" alt="close icon" />
      </button>
    </li>
  </ul>
</nav>

<style>
  nav {
    width: 100%;
    order: 1;
    background-color: #000;
    z-index: 2;
    position: absolute;
    top: 0;
    bottom: auto;
    left: 0;
  }

  nav > ul {
    display: flex;
    flex-flow: row nowrap;
    justify-content: flex-start;
    align-items: center;
    padding: 0;
    margin: 0.5rem;
  }

  nav > ul > li {
    list-style-type: none;
  }

  button {
    display: inline-block;
    background-color: #000;
    color: #fff;
    text-align: center;
    /* These two are needed for <button>*/
    border: 0;
    cursor: pointer;
  }
</style>