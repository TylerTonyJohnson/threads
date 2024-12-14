<script lang="ts">
	import { T } from '@threlte/core';
	import { Gizmo, OrbitControls } from '@threlte/extras';
	import { MeshStandardMaterial, TubeGeometry, Vector2, Vector3, CatmullRomCurve3 } from 'three';

	let {
		autoRotate,
		enableDamping,
		rotateSpeed,
		zoomToCursor,
		zoomSpeed,
		minPolarAngle,
		maxPolarAngle,
		enableZoom
	} = $props();

	let amplitude = $state(2);
	let period = $state(1);
	let segments = $state(10);
	let length = $state(100);

	// let points = [];
	// for (let i = 0; i < 10; i++) {
	// 	const x = Math.sin(i * period) * amplitude;
	// 	const y = i * 10;
	// 	const z = Math.cos(i * period) * amplitude;

	// 	points.push(new Vector3(x, y, z));
	// }

	// const path = new CatmullRomCurve3(points);

	const radius = 1;
	const threads = 3;

	const braids = [0, 1, 2, 2, 1, 0];

	const positions: any = [];
	for (let i = 0; i < threads; i++) {
		const x = Math.sin((i * Math.PI * 2) / threads) * radius;
		const z = Math.cos((i * Math.PI * 2) / threads) * radius;

		positions.push(new Vector2(x, z));
	}

	const paths: any = [];
	positions.forEach((position: any, i: any) => {
		// const phase = (i / threads) * Math.PI * 2;

		const phase = i * ((Math.PI * 2) / threads);

		const points: any = [];
		for (let j = 0; j < segments; j++) {
			// const x = positions[braids[(i + j) % 6]].x;
			const x = amplitude * Math.sin((j * Math.PI * 2) / segments + phase);
			const y = (j * length) / segments;
			// const z = positions[braids[(i + j) % 6]].y;
			const z =
				amplitude *
				Math.sin((j * Math.PI * 2) / segments + phase) *
				Math.cos((j * Math.PI * 2) / segments + phase);

			points.push(new Vector3(x, y, z));
		}

		const path = new CatmullRomCurve3(points);

		paths.push(path);
	});

	const colors = ['red', 'green', 'blue'];

	console.log(positions);
</script>

<T.PerspectiveCamera makeDefault position={[10, 5, 10]} lookAt.y={0.5}>
	<OrbitControls
		{enableDamping}
		{autoRotate}
		{rotateSpeed}
		{zoomToCursor}
		{zoomSpeed}
		{minPolarAngle}
		{maxPolarAngle}
		{enableZoom}
	/>
</T.PerspectiveCamera>
<Gizmo horizontalPlacement="left" paddingX={20} paddingY={20} />
<T.DirectionalLight position.y={10} position.z={10} />
<T.AmbientLight intensity={0.3} />
<T.GridHelper args={[10, 10]} />
<T.Group rotation.x={Math.PI}>
	{#each paths as path, i}
		<T.Mesh>
			<T.TubeGeometry args={[path, 20, 1, 16, false]} />
			<T.MeshStandardMaterial color={colors[i]} />
		</T.Mesh>
	{/each}
</T.Group>
