<script lang="ts">
	import favicon from '$lib/assets/favicon.svg';
	import 'bootstrap/dist/css/bootstrap.min.css';
	let { children } = $props();
	export const ssr = false;
	export const prerender = true;
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<div class="main">
	{@render children?.()}
</div>

<style>
	.main{
		height: 100vh;
		display: flex;
		flex-direction: column;
		justify-content: center;
	}
</style>