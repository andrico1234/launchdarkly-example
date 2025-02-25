<script>
	const { children } = $props();
</script>

<div class="panel">
	{@render children()}
</div>

<style>
	.panel {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		border: var(--panel-border);
		background-color: var(--panel-color-background);
		box-shadow: var(--panel-shadow);
		width: fit-content;
		padding: 2px;
	}
</style>
