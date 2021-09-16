<script>
	import ReleaseCard from './ReleaseCard.svelte';

	export let projectName = "corylus-git/corylus";

	$: releasesRequest = fetch(
		`https://api.github.com/repos/${projectName}/releases`
	).then((response) => {
		if(response.status !== 200) {
			return response.json().then(e => {
				throw new Error(e.message);
			});
		}
		return response.json();
	})
</script>

<main>
	<h1 class="test">GitHub project release list</h1>
	<h2>{projectName}</h2>
	<input type="text"
			bind:value={projectName} />

	{#await releasesRequest}
		Loading...
	{:then releases}
		{#each releases as release}
			<ReleaseCard {release} />
		{/each}
	{:catch e}
		<div>Could not load <em>{projectName}</em>.</div>
		<div>
			{e.message}
		</div>
	{/await}
</main>

<style>
	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}
</style>