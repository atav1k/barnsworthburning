<script context="module">
	import { FULL_API } from '../../config.js';

	export async function preload(page, session) {
		let extracts;
		let options = {
			sort: [{ field: 'last_name', direction: 'asc' }],
			fields: [
				'full_name',
				'last_name',
				'profession',
				'organization',
				'site',
				'group_names',
				'group_slugs',
			],
		};

		let creators = await this.fetch(
			`${FULL_API}/airtableGet?base=commonplace&table=creators&options=${JSON.stringify(
				options
			)}`
		)
			.then(data => data.json())
			.catch(error => {
				console.log(error);
				return [];
			});

		return { creators };
	}
</script>

<script>
	import { selectedSpace } from '../../stores';
	import Link from '../../components/Link.svelte';

	selectedSpace.set('creators');

	export let creators = undefined;
</script>

<table>
	<thead>
		<tr>
			<th>Name</th>
			<th>Homepage</th>
			<th>Professions</th>
			<th>Works</th>
		</tr>
	</thead>
	<tbody>
		{#each creators as {id, full_name, profession, group_names, group_slugs,
		site}}
		<tr>
			<td>
				<strong>{full_name}</strong>
			</td>
			<td>
				{#if site}
				<a href="{site}" target="_blank" title="{full_name}'s home page"
					>Website</a
				>
				{/if}
			</td>
			<td>{profession ? profession.join(', ') : ''}</td>
			<td>
				{#if group_names}
				<ul>
					{#each group_names as group, i}
					<li><a href="/works/{group_slugs[i]}">{group}</a></li>
					{/each}
				</ul>
				{/if}
			</td>
		</tr>
		{/each}
	</tbody>
</table>

<style>
	ul {
		margin: 0;
		padding: 0 0 0 1.2rem;
	}
</style>
