<script>
	import Header from './header.svelte';
</script>

<div class="app">
	<Header />
	<slot />
</div>

<style>
	.app {
		color: black;
		min-height: 100vh;
	}
</style>
