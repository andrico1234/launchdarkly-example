<script>
	import { onMount } from 'svelte';
	import StartButton from './start-button.svelte';

	const timeFormat = new Intl.DateTimeFormat('en-US', {
		hour: 'numeric',
		minute: 'numeric',
		second: 'numeric'
	});

	const date = new Date();

	let formattedTime = $state(timeFormat.format(date));

	let timeout;

	onMount(() => {
		timeout = setInterval(() => {
			formattedTime = timeFormat.format(new Date());
		}, 1000);
	});
</script>

<div class="taskbar">
	<StartButton />
	<div class="utility-bar">{formattedTime}</div>
</div>

<style>
	.taskbar {
		--inset-shadow-padding: 2px;

		font-family: var(--font-primary);
		letter-spacing: var(--font-primary-letter-spacing);
		box-sizing: border-box;
		border: var(--taskbar-border);
		border-top: 0;
		border-left: 0;
		box-shadow: var(--taskbar-shadow);
		background-color: var(--taskbar-color-background);
		width: 100%;
		padding: var(--taskbar-padding);
		padding-top: calc(var(--inset-shadow-padding) + var(--taskbar-padding));
		padding-left: calc(var(--inset-shadow-padding) + var(--taskbar-padding));
		height: var(--taskbar-height);
		margin-bottom: var(--inset-shadow-padding);
		display: flex;
		justify-content: space-between;
	}

	.utility-bar {
		--inset-shadow-padding: 2px;

		display: flex;
		height: 100%;
		box-sizing: border-box;
		align-items: center;
		padding: var(--taskbar-padding);
		padding-left: calc(var(--inset-shadow-padding) + var(--taskbar-padding));
		box-shadow: var(--taskbar-utility-bar-shadow);
	}
</style>
