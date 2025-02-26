<script>
	import StartMenu from './start-menu.svelte';

	let isMenuOpen = $state(false);

	const toggleMenu = () => {
		isMenuOpen = !isMenuOpen;
	};
</script>

<div class="start-button">
	<StartMenu open={isMenuOpen} />
	<button onclick={toggleMenu}>
		<img class="icon" width="32" src="/icons/w2k_wupdate_1.png" alt="Start" />
		Start
	</button>
</div>

<style>
	.start-button {
		position: relative;
		height: 100%;
	}

	button {
		display: flex;
		align-items: center;
		gap: var(--taskbar-content-gap);
		font-family: var(--font-primary);
		letter-spacing: var(--font-primary-letter-spacing);
		height: 100%;
		font-weight: var(--font-weight-heavy);
		font-size: var(--font-size-100);
		line-height: var(--font-size-100);
		background-color: var(--color-gray-600);
		cursor: var(--cursor-pointer);
		border: var(--button-border);
		border-left: 1px dotted var(--color-white);
		border-top: 1px dotted var(--color-white);
		box-shadow: var(--button-shadow);
		outline-color: var(--outline-color-focus);
		outline-offset: var(--outline-offset-focus);
	}

	button:active {
		border-bottom: 2px solid transparent;
		border-right: 0;
		border-left: 1px dotted var(--color-black);
		border-top: 1px dotted var(--color-black);
		box-shadow: var(--button-shadow-active);
		transform: translate(2px, 2px);
	}
</style>
