<script>
	import { setContext } from 'svelte';
	let node;

	setContext('modal_target', () => node);
</script>

<slot/>
<div
	bind:this={node}
	class="fixed top-0 left-0 w-screen bg-black/10 dark:bg-black/30 h-screen empty:hidden empty:bg-black/0 transition-[background-color 5000ms linear]"
/>
