<script>
	const { children } = $props();
</script>

<div id="marquee-container">
	<div id="marquee">
		<div id="marquee-inner-1">
			{@render children()}
		</div>
		<div id="marquee-inner-2">
			{@render children()}
		</div>
	</div>
</div>

<style>
	#marquee-container {
		background: var(--marquee-background);
		padding: var(--spacing-50) 0;
	}

	#marquee-container * {
		margin: 0;
	}

	#marquee {
		overflow: hidden;
		width: 100%;
		position: relative;
	}

	#marquee:hover > * {
		animation-play-state: paused;
	}

	#marquee-inner-2 {
		top: 0;
		position: absolute;
		width: 100%;
	}

	@media (prefers-reduced-motion: no-preference) {
		#marquee-inner-1 {
			animation: marquee-move var(--marquee-animation-duration) both infinite linear;
		}

		#marquee-inner-2 {
			animation: marquee-move var(--marquee-animation-duration) both
				calc(var(--marquee-animation-duration) / 2) infinite linear;
		}
	}

	@keyframes marquee-move {
		from {
			transform: translateX(100%);
		}

		to {
			transform: translateX(-100%);
		}
	}
</style>
