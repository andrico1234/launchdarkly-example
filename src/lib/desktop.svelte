<script>
	const { children } = $props();
</script>

<div id="desktop">
	{@render children()}
</div>

<style>
	#desktop {
		height: 100%;
	}
</style>
