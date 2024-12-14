<script lang="ts">
	import { Canvas } from '@threlte/core';
	import Scene from '$lib/components/Scene.svelte';
	import Settings from '$lib/config/Settings.svelte';

	let autoRotate: boolean = $state(false);
	let enableDamping: boolean = $state(true);
	let rotateSpeed: number = $state(1);
	let zoomToCursor: boolean = $state(false);
	let zoomSpeed: number = $state(1);
	let minPolarAngle: number = $state(0);
	let maxPolarAngle: number = $state(Math.PI);
	let enableZoom: boolean = $state(true);

	// let width = $state(1000);
	// let height = $state(1000);

	// let count = $state(50);
	// let phi = $state((Math.sqrt(5) + 1) / 2 - 1);
	// let fudge = $state(0.87); // Fudge factor, since our circles don't actually fill up space entirely.
	// let skip = $state(2);

	// let goldRatio = $derived(phi * 2 * Math.PI);

	// let lg_rad = $derived(width * 0.45);
	// let lg_area = $derived(Math.pow(lg_rad, 2) * Math.PI);

	// let sm_area = $derived(lg_area / count); // Area of our little circles, if they filled the space entirely
	// let sm_rad = $derived(Math.sqrt(sm_area / Math.PI)); // This is related to the equation area = pi r squared

	// function adjustedIndex(i: number) {
	// 	// return i;
	// 	return i === 0 ? 0 : i + skip;
	// }

</script>

<div class="frame">
	<!-- <svg
		xmlns="http://www.w3.org/2000/svg"
		xmlns:xlink="http://www.w3.org/1999/xlink"
		viewBox="-500 -500 1000 1000"
	>
		{#each Array(count) as _, i}
			<circle
				cx={Math.cos(adjustedIndex(i) * goldRatio) *
					Math.sqrt((adjustedIndex(i) * sm_area) / Math.PI)}
				cy={Math.sin(adjustedIndex(i) * goldRatio) *
					Math.sqrt((adjustedIndex(i) * sm_area) / Math.PI)}
				r={fudge * sm_rad}
				fill="blue"
				stroke="black"
			></circle>
		{/each}
	</svg>
	<div class="container">
		<label>
			<span>Count</span>
			<input type="range" bind:value={count} min="1" max="100" step="1" />
			<div>{count}</div>
		</label>
		<label>
			<span>Skip</span>
			<input type="range" bind:value={skip} min="0" max="10" step="1" />
			<div>{skip}</div>
		</label>
		<label>
			<span>Phi</span>
			<input type="range" bind:value={phi} min="0" max="1" step="0.001" />
			<div>{phi}</div>
		</label>
		<label>
			<span>Fudge</span>
			<input type="range" bind:value={fudge} min="0" max="2" step="0.1" />
			<div>{fudge}</div>
		</label>
	</div> -->
	<Canvas>
		<Scene
			{enableDamping}
			{autoRotate}
			{rotateSpeed}
			{zoomToCursor}
			{zoomSpeed}
			{minPolarAngle}
			{maxPolarAngle}
			{enableZoom}
		/>
	</Canvas>
	<Settings
		bind:enableDamping
		bind:autoRotate
		bind:rotateSpeed
		bind:zoomToCursor
		bind:zoomSpeed
		bind:minPolarAngle
		bind:maxPolarAngle
		bind:enableZoom
	/>
</div>

<style>
	.frame {
		display: flex;
		gap: 1rem;
		justify-content: center;
		align-items: center;
		height: 100%;
	}

	.container {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		/* height: 100%; */
		padding: 1rem;
		gap: 1rem;
		border: solid black 2px;
		/* background-color: purple; */
	}

	svg {
		border: 1px solid black;
		width: 1000px;
		height: 1000px;
	}
</style>
