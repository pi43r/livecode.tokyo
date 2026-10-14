<script>
	import './layout.css';

	/** @type {{children: import('svelte').Snippet}} */
	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" type="image/svg+xml" href="/lct.svg" />
</svelte:head>

{@render children()}
