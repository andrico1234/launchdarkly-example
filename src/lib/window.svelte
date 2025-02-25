<script>
	import Panel from './panel.svelte';

	const { heading, children } = $props();
</script>

<Panel>
	<div class="stack">
		{@render children()}
	</div>
</Panel>
