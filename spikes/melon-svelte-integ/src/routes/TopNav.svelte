<script lang="ts">
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
<nav>
  <ul>
    <li><button onclick={onMenuOne}>Menu One</button></li>
    <li><button onclick={onMenuTwo}>Menu Two</button></li>
    <li><button onclick={onMenuThree}>Menu Three</button></li>
  </ul>
</nav>

<style>
	nav {
		width: 100%;
		order: -1;
		background-color: rgba(28 33 169 / 0.22);
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
</style>