<script>
	import { fade, blur } from 'svelte/transition';
	import { onMount } from 'svelte';

	let rendered = false;

	// const LOADING = [
	// 	['', '', '', '', 'I', '', ''],
	// 	['', '', '', '', 'I', 'N', ''],
	// 	['', '', '', 'D', 'I', 'N', ''],
	// 	['', '', 'A', 'D', 'I', 'N', ''],
	// 	['', '', 'A', 'D', 'I', 'N', 'G'],
	// 	['', 'O', 'A', 'D', 'I', 'N', 'G'],
	// 	['L', 'O', 'A', 'D', 'I', 'N', 'G']
	// ];
	const HOLDON = [
		['H', 'O', 'L', 'D', 'O', 'N'],
		['H', 'O', 'L', 'D', '', 'N'],
		['H', '', 'L', 'D', '', 'N'],
		['H', '', 'L', 'D', '', ''],
		['', '', 'L', 'D', '', ''],
		['', '', 'L', '', '', '']
	];

	const interval = 100; // ms
	const duration = 500;

	const grid = HOLDON.map((row, i) => {
		return row.map((cell, j) => {
			return {
				content: cell,
				delay: (i + 1) * j * interval,
				duration
			};
		});
	});

	onMount(() => {
		rendered = true;
	});

	const getGridArea = (i, j) => {
		return `grid-area: ${i + 1} / ${j + 1}`;
	};
</script>

<div class="loading loading--outer text-mono">
	{#if rendered}
	<div transition:fade class="loading--inner">
		{#each grid as row, i} {#each row as {content, delay}, j}
		<span in:blur="{{delay, duration}}" out:fade>
			{content}
		</span>
		{/each} {/each}
	</div>
	{/if}
</div>

<style>
	.loading--outer {
		grid-area: loading;
		position: absolute;
		top: 0;
		right: 0;
		bottom: 0;
		left: 0;
		display: flex;
		justify-content: center;
		align-items: center;
		pointer-events: none;
	}
	.loading--inner {
		display: inline-grid;
		grid-template-rows: repeat(6, 2em);
		grid-template-columns: repeat(6, 2em);
		grid-gap: 4px;
		place-items: center;
		/* -webkit-backdrop-filter: blur(4px);
		backdrop-filter: blur(4px); */
	}
	span {
		display: flex;
		height: 100%;
		width: 100%;
		justify-content: center;
		align-items: center;
		border: 1px solid var(--divider);
		background-color: var(--layer-bg);
	}

	@media (max-width: 950px) {
		.loading--outer {
			margin: 1rem;
		}
		.loading--inner {
			width: 100%;
			height: 100%;
			max-height: 200px;
			grid-template-rows: repeat(3, 1fr);
			grid-template-columns: repeat(12, 1fr);
		}
	}
</style>
