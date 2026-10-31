<script lang="ts">
	import { WEB_READER_URL } from '#lib/config.js';
	import { onMount } from 'svelte';

	onMount(() => {
		window.location.href = WEB_READER_URL;
	});
</script>

<svelte:head>
	<title>Opening Bible Web Reader...</title>
	<meta http-equiv="refresh" content="0; url={WEB_READER_URL}" />
</svelte:head>

<div class="redirect-wrap">
	<p>Redirecting to the <strong>Bible Web Reader</strong>...</p>
	<p>If you are not redirected, <a href={WEB_READER_URL}>click here to open the web reader</a>.</p>
</div>

<style>
	.redirect-wrap {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		min-height: 50vh;
		text-align: center;
		padding: 40px 20px;
		font-family: var(--sans, system-ui, sans-serif);
		color: var(--fg, #e6e6e8);
	}
	a {
		color: #5d87ff;
		text-decoration: underline;
	}
</style>
