<script lang="ts">
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();

	function onMenuOne() {
		console.debug("onMenuOne");
	}

	function onMenuTwo() {
		console.debug("onMenuTwo");
	}

	function onMenuThree() {
		console.debug("onMenuThree");
	}
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<div class="container">
	<nav>
		<ul>
			<li><button onclick={onMenuOne}>Menu One</button></li>
			<li><button onclick={onMenuTwo}>Menu Two</button></li>
			<li><button onclick={onMenuThree}>Menu Three</button></li>
		</ul>
	</nav>
	
	<main>
		{@render children?.()}
	</main>
</div>

<style>
	.container {
		height: 100%;
		display: flex;
		flex-flow: column nowrap;
    justify-content: flex-start;
	}

	nav {
		width: 100%;
		order: -1;
		background-color: transparent;
		z-index: 2;
		position: absolute;
		top: 0;
		left: 0;
	}

	nav > ul {
		display: flex;
    flex-flow: row nowrap;
    justify-content: space-between;
		padding: 0;
	}

	nav > ul > li {
		list-style-type: none;
	}

	nav > ul > li > button {
		padding: 0;
		margin: 0;
	}

	main {
    width: 100%;
    margin: 0;
    overflow-y: auto;
		z-index: 1;
  }
</style>