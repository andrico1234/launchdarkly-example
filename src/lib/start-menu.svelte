<script>
	import Panel from './panel.svelte';
	import { goto } from '$app/navigation';

	const { open } = $props();
</script>

<div id="start-menu" class={open ? 'open' : ''}>
	<Panel>
		<div id="content">
			<div id="side-strip">
				<p>Andricos2000</p>
			</div>
			<div id="stack-wrapper" style="align-self: flex-end;">
				<div class="stack">
					<button style="width: 100%;" onclick={() => goto('/')}>
						<div id="start-menu-item">
							<div id="icon-wrapper">
								<img src="/icons/w2k_shut_down.png" alt="Shut Down" />
							</div>
							<p id="text-wrapper">Shut Down</p>
						</div>
					</button>
				</div>
			</div>
		</div>
	</Panel>
</div>

<style>
	#start-menu {
		position: absolute;
		bottom: calc(0px + var(--taskbar-height));
		display: none;
		left: 0;
	}

	#start-menu.open {
		display: block;
	}

	#content {
		width: var(--start-menu-height);
		display: flex;
		flex-direction: row;
	}

	#stack-wrapper {
		flex-grow: 1;
	}

	#side-strip {
		writing-mode: vertical-rl;
		transform: rotate(180deg);
		background: var(--start-menu-strip-background-gradient);
		padding-block-top: var(--spacing-100);
	}

	button {
		background: none;
		border: 0;
		margin: 0;
		padding: 0;
		font-family: var(--font-primary);
		letter-spacing: var(--font-primary-letter-spacing);
		font-size: var(--font-size-100);
	}

	#side-strip p {
		color: white;
		font-weight: var(--font-weight-600);
		margin: 0;
		padding-inline-start: var(--spacing-50);
	}

	#start-menu-item {
		height: var(--start-menu-item-height);
		box-sizing: border-box;
		display: flex;
		align-items: center;
		padding-inline: var(--start-menu-item-padding);
		gap: var(--start-menu-item-gap);
		background: var(--start-menu-item-background);
		cursor: var(--cursor-pointer);
		width: 100%;
		border: 0;
		font-size: inherit;
		text-align: left;
		font-family: var(--font-primary);
		letter-spacing: var(--font-primary-letter-spacing);
	}

	#start-menu-item:hover {
		background: var(--start-menu-background-hover);
	}

	#start-menu-item:hover p {
		color: var(--start-menu-item-text-color-hover);
	}

	#icon-wrapper {
		width: var(--start-menu-icon-size);
		height: var(--start-menu-icon-size);
	}

	#start-menu.open {
		display: block;
	}

	#text-wrapper {
		flex: 1;
		margin: 0;
	}
</style>
