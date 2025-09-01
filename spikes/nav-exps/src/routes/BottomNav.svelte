<script lang="ts">
  import { page } from "$app/state";
  import homeIconFill from "$lib/assets/home-icon-fill.svg";
  import homeIconOutline from "$lib/assets/home-icon-outline.svg";
  import friendsIconFill from "$lib/assets/friends-icon-fill.svg";
  import friendsIconOutline from "$lib/assets/friends-icon-outline.svg";
  import notifsIconFill from "$lib/assets/notifs-icon-fill.svg";
  import notifsIconOutline from "$lib/assets/notifs-icon-outline.svg";
  import profileIconFill from "$lib/assets/profile-icon-fill.svg";
  import profileIconOutline from "$lib/assets/profile-icon-outline.svg";

  let currPage = page.url.pathname as string;
  let homeIcon = currPage === "/" ? homeIconFill : homeIconOutline;
  let friendsIcon = currPage === "/friends" ? friendsIconFill : friendsIconOutline;
  let notifsIcon = currPage === "/notifs" ? notifsIconFill : notifsIconOutline;
  let profileIcon = currPage === "/profile" ? profileIconFill : profileIconOutline;

</script>

<nav>
  <ul>
    <li 
			class="menu-item" 
			aria-current={page.url.pathname as string === "/explore" ? "page" : undefined}
		>
			<a href="/">
        <img src="{homeIcon}" alt="home icon" />
        <br />
        Home
      </a>
		</li>
    <li 
			class="menu-item" 
			aria-current={page.url.pathname as string === "/favorites" ? "page" : undefined}
		>
			<a href="/">
        <img src="{friendsIcon}" alt="friends icon" >
        <br />
        Friends
      </a>
		</li>
    <li 
			class="menu-item" 
			aria-current={page.url.pathname as string === "/" ? "page" : undefined}
		>
			<a href="/">
        <img src="{notifsIcon}" alt="notifs icon" />
        <br />
        Notifs
      </a>
		</li>
		<li 
			class="menu-item search" 
			aria-current={page.url.pathname as string === "/search" ? "page" : undefined}
		>
			<a href="/">
        <img src="{profileIcon}" alt="profile icon" />
        <br />
				Profile
			</a>
		</li>
  </ul>
</nav>

<style>
  nav {
    width: 100%;
    order: 1;
    background-color: transparent;
    z-index: 2;
    position: absolute;
    top: auto;
    bottom: 0;
    left: 0;
    font-size: 0.75rem;
  }

  nav > ul {
    display: flex;
    flex-flow: row nowrap;
    justify-content: space-around;
    align-items: flex-end;
    padding: 0;
    margin: 0.5rem;
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
  }
</style>