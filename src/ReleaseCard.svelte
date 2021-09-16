<script>
	import Markdown from "svelte-markdown";

    export let release;
</script>

<div class="card">
    <div class="header">
        <a href={release.html_url}>{release.name}</a>, published on {release.published_at}
    </div>
    <div class="description">
        <Markdown source={release.body} />
    </div>
</div>

<style>
	.card {
		width: 60em;
		border-radius: 2px;
		border: 1px solid #a0a0a0;
		box-shadow: 2px 2px 2px rgba(0, 0, 0, 0.2);
		margin: 1em;
	}

	.header {
		border-bottom: 1px dotted black;
		font-size: 120%;
	}

	.description {
		padding: 1em;
	}
</style>