<script>
	import BlueScreen from '$lib/blue-screen.svelte';
	import Desktop from '$lib/desktop.svelte';
	import IconButton from '$lib/icon-button.svelte';
	import Minesweeper from '$lib/minesweeper.svelte';
	import Taskbar from '$lib/taskbar.svelte';

	let isMinesweeperOpen = $state(false);
	let isBlueScreenOpen = $state(false);
	const openMinesweeper = () => {
		isMinesweeperOpen = true;
	};

	const showBlueScreen = () => {
		isBlueScreenOpen = true;
	};
</script>

<div id="app" class="cover">
	<Desktop>
		<IconButton icon="w2k_computer" text="Minesweeper" onOpen={openMinesweeper} />
	</Desktop>
	<Taskbar />

	{#if isMinesweeperOpen}
		<Minesweeper onPress={showBlueScreen} />
	{/if}
</div>

{#if isBlueScreenOpen}
	<BlueScreen />
{/if}
