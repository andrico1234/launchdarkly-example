<script>
	import Panel from './panel.svelte';

	const { heading, children } = $props();
</script>

<div class="window">
	<Panel>
		<div class="heading-wrapper">
			<h2 class="heading">
				{heading}
			</h2>
		</div>
		<div class="stack">
			{@render children()}
		</div>
	</Panel>
</div>

<style>
	.window {
		position: absolute;
		left: 32px;
		top: 32px;
	}
	.heading-wrapper {
		background: var(--window-topbar-background);
		user-select: none;
		height: var(--window-topbar-height);
		display: flex;
		align-items: center;
	}

	h2 {
		margin: 0;
		font-size: var(--window-topbar-heading-font-size);
		color: var(--window-topbar-heading-color);
		padding: 0 var(--window-spacing-horizontal);
	}
</style>
