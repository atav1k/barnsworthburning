<script>
	import Link from './Link.svelte';

	import About from './icons/About.svelte';

	import Spaces from './icons/Spaces.svelte';
	import Extracts from './icons/Extracts.svelte';
	import Works from './icons/Works.svelte';
	import Creators from './icons/Creators.svelte';

	let links = [
		{
			path: undefined,
			title: 'Spaces',
			icon: Spaces
		},
		{
			path: 'extracts',
			title: 'Extracts',
			icon: Extracts
		},
		{
			path: 'works',
			title: 'Works',
			icon: Works
		},
		{
			path: 'creators',
			title: 'Creators',
			icon: Creators
		}
	];
	export let currentPage = undefined;
</script>

<nav class="themey">
	<ul>
		{#each links as {path, title, icon}}
		<li>
			<Link active="{currentPage === path}" className="nav-link" prefetch href="{path || '/'}" {title}>
				<span role="presentation" class="pointer">‹‹‹</span>
				<span role="presentation" class="space">&nbsp;</span>
				<svelte:component this={icon} />
				<span class="title">{title}</span>
				<span role="presentation" class="space">&nbsp;</span>
				<span role="presentation" class="pointer">›››</span>
			</Link>
		</li>
		{/each}
	</ul>
</nav>

<style>
	nav {
		padding: 0.25rem 1rem;
		border-radius: 4rem;
		box-shadow: 0 -3px 6px rgba(0,0,0,0.25);
	}

	ul {
		list-style-type: none;
		margin: 0;
		padding: 0;
		display: flex;
		flex-wrap: wrap;
		align-items: center;
		justify-content: space-around;
	}

	li {
		white-space: nowrap;
		margin: 0 1rem;
		display: inline-flex;
	}

	li > :global(.nav-link) {
		display: inline-flex;
	}

	li > :global(.nav-link.active) {
		flex-direction: row-reverse;
	}

	li :global(.icon) {
		height: 1.5rem;
		display: none;
		opacity: 0.9;
	}

	.title {
		text-transform: uppercase;
	}

	@media(max-width: 1080px) {
		.pointer,
		.space {
			display: none;
		}
	}

	@media(max-width: 600px) {
		.title {
			display: none;
		}
		li :global(.icon) {
			display: inline-block;
		}
	}
</style>