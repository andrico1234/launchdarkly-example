<script lang="ts">
	import { onMount } from 'svelte';
	import ProgressUnit from './progress-unit.svelte';

	const { progress = 0 } = $props();

	const getRemainder = (number: number) => {
		return Math.floor((number % 1) * 10) / 10;
	};

	let elCount = $state(0);
	let elArray = $derived(Array(elCount).fill(progress));
	let width = $state(0);

	let ref: HTMLDivElement;

	let unitsToDisplayDecimal = $derived((progress / 100) * elCount);

	const remainder = $derived(getRemainder(unitsToDisplayDecimal));
	const unitsToDisplay = $derived(Math.floor(unitsToDisplayDecimal));

	onMount(() => {
		const newWidth = ref.getBoundingClientRect().width ?? 0;

		if (newWidth === width) return;

		width = newWidth;

		const { gap } = getComputedStyle(ref);
		const gapNumber = Number(gap.replace('px', ''));
		const elWidth = gapNumber + 12;
		elCount = Math.ceil(width / elWidth);
	});
</script>

<div bind:this={ref} aria-label="Loading progress" id="progress" role="progressbar">
	{#each elArray as _, i}
		{#if i < unitsToDisplay}
			<ProgressUnit filled="full" />
		{:else if i === unitsToDisplay && remainder >= 0.5}
			<ProgressUnit filled="half-filled" />
		{:else}
			<ProgressUnit filled="none" />
		{/if}
	{/each}
</div>

<style>
	#progress {
		width: 100%;
		box-sizing: border-box;
		display: flex;
		box-shadow: var(--progress-shadow);
		padding-left: 3px;
		padding-right: 1px;
		padding-bottom: 2px;
		padding-top: 3px;
		height: var(--progress-height);
		border-right: var(--progress-border-right);
		gap: var(--progress-contents-gap);
		overflow: hidden;
	}
</style>
