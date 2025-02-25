<script>
	import Panel from './panel.svelte';

	const { onPress } = $props();

	const GRID_SIZE = 10;
	let grid = Array(GRID_SIZE)
		.fill(null)
		.map(() => Array(GRID_SIZE).fill(null));
</script>

<Panel>
	<div class="grid">
		{#each grid as row, i}
			{#each row as cell, j}
				<button class="cell" onclick={() => onPress()} />
			{/each}
		{/each}
	</div>
</Panel>

<style>
	.grid {
		display: grid;
		grid-template-columns: repeat(10, 1fr);
		gap: 2px;
		max-width: 400px; /* adjust as needed */
	}

	.cell {
		aspect-ratio: 1;
		width: 100%;
	}
</style>
