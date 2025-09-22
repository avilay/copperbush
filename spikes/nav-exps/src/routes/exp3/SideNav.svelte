<script lang="ts">
  import starIconOutline from "$lib/assets/star-icon-outline.svg";
  import commentIconOutline from "$lib/assets/comment-icon-outline.svg";
  import friendAddIconOutline from "$lib/assets/friend-add-icon-outline.svg";

  let { game } = $props();
  
  const starCount = Intl.NumberFormat('en-US', {
    notation: "compact",
    maximumFractionDigits: 1
  }).format(game.starCount);

  const commentCount = Intl.NumberFormat("en-US", {
    notation: "compact",
    maximumFractionDigits: 1
  }).format(game.commentCount);
</script>

<nav>
  <ul>
    <li class="menu-item">
      <a href="/dev">
        <img class="profile" src="{game.logoUrl}" alt="logo of game developer" />
      </a>
    </li>
    <li class="menu-item">
      <a href="/star">
        <div>
          <img class="icon" src="{starIconOutline}" alt="star icon" />
          {starCount}
        </div>
      </a>
    </li>
    <li class="menu-item">
      <a href="/comments">
        <div>
          <img class="icon" src="{commentIconOutline}" alt="comment icon" />
          {commentCount}
        </div>
      </a>
    </li>
    <li class="menu-item">
      <a href="/invite">
        <div><img class="icon" src="{friendAddIconOutline}" alt="invite friend icon" /></div>
      </a>
    </li>
  </ul>
</nav>

<style>
  nav {
    background-color: transparent;
    position: absolute;
    right: 5px;
    top: 50%;
    transform: translateY(-50%);
    z-index: 10;
  }

  nav > ul {
    display: flex;
    flex-flow: column nowrap;
    justify-content: flex-start;
    align-items: center;
    gap: 2em;
    padding: 0;
    margin: 0.25em;
  }

  .menu-item {
    list-style-type: none;
  }

  .menu-item > a {
    padding: 0;
    margin: 0;
    font-family: inherit;
    text-decoration: none;
    text-align: center;
    color: #fff;
    font-size: 0.8rem;
  }

  .profile {
    width: 64px;
    height: 64px;
    border-radius: 50%; /* Makes the image circular */
    object-fit: cover; /* Ensures the image covers the area without distortion */
  }

  .icon {
    width: 32px;
    height: 32px;
    display: block;
  }
</style>