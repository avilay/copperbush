<script lang="ts">
	import { page } from '$app/state';
	
	import searchicon from "$lib/assets/searchicon.svg";

	function onMenuOne() {
		console.debug("onMenuOne");
	}

	function onMenuTwo() {
		console.debug("onMenuTwo");
	}

	function onMenuThree() {
		console.debug("onMenuThree");
		console.log(page.url.pathname);
	}
</script>
<nav>
  <ul>
    <li 
			class="menu-item" 
			aria-current={page.url.pathname as string === "/explore" ? "page" : undefined}
		>
			<a href="/">Explore</a>
		</li>
    <li 
			class="menu-item" 
			aria-current={page.url.pathname as string === "/starred" ? "page" : undefined}
		>
			<a href="/">Starred</a>
		</li>
    <li 
			class="menu-item" 
			aria-current={page.url.pathname as string === "/" ? "page" : undefined}
		>
			<a href="/">For You</a>
		</li>
		<li 
			class="menu-item search" 
			aria-current={page.url.pathname as string === "/search" ? "page" : undefined}
		>
			<a href="/">
				<img src="{searchicon}" alt="search icon">
			</a>
		</li>
  </ul>
</nav>

<style>
	nav {
		width: 100%;
		order: -1;
		/* background-color: rgba(41 41 41 / 0.8); */
		background-color: transparent;
		z-index: 2;
		position: absolute;
		top: 0;
		left: 0;
	}

	nav > ul {
		display: flex;
    flex-flow: row nowrap;
    justify-content: space-evenly;
		align-items: center;
		padding: 0;
		margin: 0.5em;
	}

	.menu-item {
		list-style-type: none;
	}

	.menu-item > a {
		padding: 0;
		margin: 0;
		text-decoration: none;
		color: #fff;
		font-family: OpenSansNarrow;
	}

	.menu-item > a:hover, .menu-item > a:focus {
		text-decoration: underline;
	}

	.menu-item[aria-current='page'] > a {
		font-weight: bold;
		text-decoration: underline;
	}
</style>