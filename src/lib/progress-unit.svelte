<script>
	const { filled = 'none' } = $props();

	const halfFilledClass = filled !== 'none' ? 'half-filled' : '';
	const filledClass = filled === 'full' ? 'filled' : '';
</script>

<div class={`${halfFilledClass} ${filledClass}`} id="unit">
	<div></div>
	<div></div>
</div>

<style>
	#unit {
		width: var(--progress-unit-width);
		height: 100%;
		display: flex;
		flex-direction: row;
	}

	#unit > div {
		width: calc(var(--progress-unit-width) / 2);
		height: 100%;
	}

	.half-filled > div:first-child {
		background: var(--progress-unit-background);
	}

	.filled > :last-child {
		background: var(--progress-unit-background);
	}
</style>
