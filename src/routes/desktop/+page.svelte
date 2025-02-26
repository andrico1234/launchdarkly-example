<script>
	import * as LDClient from 'launchdarkly-js-client-sdk';
	import { goto } from '$app/navigation';
	import BlueScreen from '$lib/blue-screen.svelte';
	import Desktop from '$lib/desktop.svelte';
	import IconButton from '$lib/icon-button.svelte';
	import Minesweeper from '$lib/minesweeper.svelte';
	import Taskbar from '$lib/taskbar.svelte';
	import { onMount } from 'svelte';

	let showMinesweeper = $state(false);

	let isMinesweeperOpen = $state(false);
	let isBlueScreenOpen = $state(false);
	const openMinesweeper = () => {
		isMinesweeperOpen = true;
	};

	const showBlueScreen = () => {
		isBlueScreenOpen = true;
	};

	onMount(() => {
		const context = {
			kind: 'user',
			anonymous: true
		};

		const client = LDClient.initialize('67b9e826ecf6960bf4932f18', context);

		client.on('initialized', function () {
			showMinesweeper = client.variation('enable-minesweeper', false);
			client.on('enable-minesweeper', (val) => {
				showMinesweeper = val;
			});
		});
	});
</script>

<div id="app" class="cover">
	<Desktop>
		<IconButton icon="w2k_shut_down" text="Shut Down" onOpen={() => goto('/')} />

		{#if showMinesweeper}
			<IconButton icon="w2k_computer" text="Minesweeper" onOpen={openMinesweeper} />
		{/if}
	</Desktop>
	<Taskbar />

	{#if isMinesweeperOpen}
		<Minesweeper onPress={showBlueScreen} />
	{/if}
</div>

{#if isBlueScreenOpen}
	<BlueScreen />
{/if}
