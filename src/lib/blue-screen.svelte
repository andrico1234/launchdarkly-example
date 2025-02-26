<script>
	import { goto } from '$app/navigation';

	const handleRestart = () => {
		goto('/');
	};
</script>

<div id="blue-screen">
	<div class="cover">
		<div class="heading">
			<div class="stack">
				<p>
					An error has occurred and Andricos2000 has been shut down to prevent damage to your
					browser.
				</p>
				<p>
					If this the first time you're seeing this error, please restart Andricos2000 by pressing
					Ctrl+Alt+Delete.
				</p>
				<p>
					If you continue to experience problems, please perform a fresh reinstall of Andricos2000
					using an official installation CD.
				</p>
				<div>
					<button onclick={handleRestart}>Restart</button>
				</div>
			</div>
		</div>
	</div>
</div>

<style>
	#blue-screen {
		background: var(--blue-screen-color-background);
		position: absolute;
		inset: 0;
		padding: 16px;
	}

	.stack {
		display: flex;
		flex-direction: column;
		gap: 32px;
		padding-top: 32px;
		max-width: 70ch;
	}

	.stack p {
		margin: 0;
	}

	.heading {
		color: var(--blue-screen-font-color);
		font-weight: var(--blue-screen-font-weight);
		font-size: var(--blue-screen-font-size);
	}
</style>
