<script lang="ts">
  import starIconOutline from "$lib/assets/star-icon-outline.svg";
  import commentIconOutline from "$lib/assets/comment-icon-outline.svg";
  import friendAddIconOutline from "$lib/assets/friend-add-icon-outline.svg";

  let { game } = $props();
  console.log(game);
  console.log(game.starCount);
</script>

<nav>
  <ul>
    <li class="menu-item">
      <a href="/dev">
        <img id="gamedev" src="{game.logoUrl}" alt="game dev profile" />
      </a>
    </li>
    <li class="menu-item">
      <a href="/">
        <div>
          <img src={starIconOutline} alt="star icon" />
          {game.starCount}
        </div>
      </a>
    </li>
    <li class="menu-item">
      <a href="/comments">
        <div>
          <img src={commentIconOutline} alt="comment icon" />
          {game.commentCount}
        </div>
      </a>
    </li>
    <li class="menu-item">
      <a href="/invite">
        <img src={friendAddIconOutline} alt="invite friend icon" />
      </a>
    </li>
  </ul>
</nav>

<style>
  nav {
    background-color: transparent;
    z-index: 2;
    position: absolute;
    bottom: 5rem;
    right: 0;
  }

  nav > ul {
    display: flex;
    flex-flow: column nowrap;
    justify-content: flex-start;
    align-items: center;
    gap: 2em;
    padding: 0;
    margin: 0.25em;
    font-size: 0.75rem;
  }

  .menu-item {
    list-style-type: none;
  }

  .menu-item > a {
    padding: 0;
    margin: 0;
    font-family: inherit;
    color: #fff;
    text-decoration: none;
    text-align: center;
  }

  .menu-item img {
    display: block;
  }

  #gamedev {
    border-radius: 50%;
  }
</style>