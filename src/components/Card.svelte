<script>
	export let className = undefined;
	export let onClick = undefined;
</script>

<section
	class:card="{true}"
	class="{className}"
	class:clickable="{typeof onClick === 'function'}"
	on:click="{onClick}"
>
	<slot></slot>
</section>

<style>
	section {
		background-color: var(--layer-container);
		padding: 1rem 1.5rem;
		box-shadow: 0 1px 1rem var(--clr-darker-20);
		border: var(--container-border);
		border-radius: var(--container-border-radius);
		overflow: hidden;
		transition: border-radius 0.5s, box-shadow 0.25s, background-color 0.25s;
	}

	.clickable:hover {
		background-color: var(--layer-container-hover);
		cursor: pointer;
		box-shadow: 0 1px 1.5rem var(--clr-darker-20);
	}
</style>
