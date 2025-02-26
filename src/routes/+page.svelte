<script>
	import { goto } from '$app/navigation';
	import * as LDClient from 'launchdarkly-js-client-sdk';
	import { onMount } from 'svelte';
	import generateSteps from '$lib/helpers/generateSteps';
	import roundNumber from '$lib/helpers/roundNumber';
	import Marquee from '$lib/marquee.svelte';
	import Progress from '$lib/progress.svelte';

	let isLoading = $state(false);
	let progress = $state(0);
	let currentStep = $state(0);

	const startupTime = 3000;
	const interval = 50;

	function handleStart() {
		isLoading = true;
		beginLoading();
	}

	function playStartupSound() {
		const audio = new Audio('/andricos-2000-startup.mp3');
		audio.volume = 0.3;
		audio.play();
	}

	function beginLoading() {
		const steps = generateSteps(startupTime, interval);
		playStartupSound();

		const intervalRef = setInterval(() => {
			const currentVal = steps[currentStep] ?? 0;
			const newProgress = roundNumber(progress + currentVal);

			if (newProgress >= 100) {
				clearInterval(intervalRef);
				progress = 100;
				goto('/desktop');
			} else {
				progress = newProgress;
				currentStep++;
			}
		}, interval);
	}

	let showSite = $state(false);

	onMount(() => {
		const context = {
			kind: 'user',
			anonymous: true
		};

		const client = LDClient.initialize('67b9e826ecf6960bf4932f18', context);

		client.on('initialized', function () {
			showSite = client.variation('rollout-site', false);
			client.on('rollout-site', (val) => {
				showSite = val;
			});
		});
	});
</script>

<div class="page">
	<div id="startup-background">
		<div class="cover" style="overflow: hidden;">
			{#if !showSite}
				<div class="principal">
					<div class="marquee-wrapper">
						<Marquee>
							<h1 class="marquee-text">Under Construction</h1>
						</Marquee>
					</div>
				</div>
			{:else if !isLoading}
				<div class="principal">
					<div class="content">
						<h1 id="standing-by">Standing by...</h1>
						<button data-size="large" onclick={handleStart}>Start</button>
					</div>
				</div>
				<div class="footer"></div>
			{:else}
				<div class="principal">
					<h1>Welcome. Andricos2000 is starting up...</h1>
				</div>
				<div class="footer">
					<a2k-stack>
						<div id="progress-wrapper">
							<Progress {progress}></Progress>
						</div>
						<p>{Math.floor(progress)}%</p>
						<p>Copyright Ⓒ 1999-2000. Andricos2000</p>
					</a2k-stack>
				</div>
			{/if}
		</div>
	</div>
</div>

<style>
	.page {
		--progress-unit-background: var(--color-white);

		color: var(--color-white);
		text-align: center;
		font-family: var(--font-primary);
		width: 100%;
	}

	#startup-background {
		background: var(--startup-background);
	}

	#progress-wrapper {
		max-width: var(--startup-progress-bar-width);
		margin: 0 auto;
		width: 100%;
	}

	#standing-by {
		animation: flash 0.5s infinite alternate;
	}

	button {
		width: fit-content;
		margin-inline: auto;
	}

	.content {
		display: flex;
		flex-direction: column;
		gap: var(--spacing-200);
	}

	.cover {
		padding: 1rem;
	}

	.marquee-wrapper {
		rotate: 45deg;
		scale: 2;
		overflow: hidden;
	}

	.marquee-text {
		color: var(--color-black);
		text-align: left;
		margin: 0;
	}

	@keyframes flash {
		from {
			opacity: 0;
		}

		to {
			opacity: 1;
		}
	}
</style>
