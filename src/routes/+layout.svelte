<script lang="ts">
	import favicon from '$lib/assets/favicon.svg';
    import Footer from '$lib/components/footer.svelte';
	import Header from '$lib/components/header.svelte';
	import 'bootstrap/dist/css/bootstrap.min.css';
	let { children } = $props();
	export const prerender = true;
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<div class="d-flex justify-content-between flex-column container-fluid min-vh-100">
	<Header /> 
	<div class="d-flex justify-content-center flex-grow-1 flex-column ">
		{@render children?.()}
	</div>
	<Footer />
</div>

<style>

	::view-transition-old(root) {
  		animation-delay: 500ms;
	}

	::view-transition-new(root) {
  		animation: circle-in 500ms;
	}

	@keyframes circle-in {
  		from { clip-path: circle(0% at 50% 0%); }
  		to { clip-path: circle(150% at 50% 0%); }
	}
</style>