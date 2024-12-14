<script lang="ts">
	import type { Snippet } from 'svelte';
	import type { LayoutData } from './$types';

	let { data, children }: { data: LayoutData; children: Snippet } = $props();
</script>

{@render children()}

<style>
	:global(html) {
		width: 100%;
		height: 100%;
	}

	:global(body) {
		margin: 0;
		padding: 0;
		width: 100%;
		height: 100%;
	}
</style>
