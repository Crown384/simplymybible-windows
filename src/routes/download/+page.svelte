<script lang="ts">
	import { WINDOWS_DOWNLOAD_URL } from '#lib/config.js';
	import { onMount } from 'svelte';

	onMount(() => {
		window.location.href = WINDOWS_DOWNLOAD_URL;
	});
</script>

<svelte:head>
	<title>Downloading Bible for Windows...</title>
	<meta http-equiv="refresh" content="0; url={WINDOWS_DOWNLOAD_URL}" />
</svelte:head>

<div class="redirect-wrap">
	<p>Your download of <strong>Bible for Windows</strong> should begin automatically.</p>
	<p>If it does not start, <a href={WINDOWS_DOWNLOAD_URL}>click here to download directly</a>.</p>
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
