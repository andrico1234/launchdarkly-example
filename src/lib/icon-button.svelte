<script>
	const { icon, text, onOpen } = $props();

	const isTouchDevice = () => {
		if (typeof window !== 'undefined') {
			return 'ontouchstart' in window || navigator.maxTouchPoints > 0;
		}
		return false;
	};

	const handleClick = () => {
		if (isTouchDevice()) {
			onOpen();
		}
	};

	const handleDblClick = () => {
		if (!isTouchDevice()) {
			onOpen();
		}
	};
</script>

<button class="icon-wrapper" onclick={handleClick} ondblclick={handleDblClick}>
	<img class="icon" src="/icons/{icon}.png" alt={text} />
	<p>{text}</p>
</button>

<style>
	.icon-wrapper {
		all: unset;
		box-sizing: border-box;
		display: flex;
		flex-direction: column;
		font-family: var(--font-primary);
		letter-spacing: var(--font-primary-letter-spacing);
		color: var(--desktop-icon-text-color);
		padding: var(--desktop-icon-padding);
		cursor: var(--cursor-pointer);
		gap: var(--desktop-icon-flex-gap);
		text-align: center;
		min-width: var(--desktop-icon-width);
		font-size: var(--desktop-icon-text-size);
		user-select: none;
	}

	.icon {
		width: var(--desktop-icon-width);
	}

	.icon-wrapper:active {
		border: none;
		transform: none;
		box-shadow: none;
	}

	.icon-wrapper p {
		padding: var(--desktop-icon-text-padding);
		margin: 0;
		font-size: 16px;
	}

	.icon-wrapper:focus p {
		outline: var(--desktop-icon-text-outline-focus);
		background: var(--desktop-icon-text-background-color-focus);
		color: var(--desktop-icon-text-color-focus);
	}
</style>
