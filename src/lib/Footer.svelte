<script lang="ts">
	import { resolve } from '$app/paths';
	import type { Snippet } from 'svelte';
	import { NAME } from './config.js';

	let { children }: { children?: Snippet } = $props();
</script>

<footer class="footer">
	<div class="brand">
		<img src="/icon.png" width="20" height="20" alt="" />
		<span>{NAME}</span>
	</div>
	<p>Made by <a href="https://x.com/stephtioluwani" target="_blank" rel="noopener noreferrer">Stephen</a>. {@render children?.()}</p>
	<div class="links">
		<a href="/privacy">Privacy</a>
		<a href="/support">Support</a>
	</div>
</footer>

<style>
	.footer {
		display: flex;
		align-items: center;
		gap: 24px;
		max-width: 1080px;
		margin: 0 auto;
		padding: 32px 24px 48px;
		border-top: 1px solid var(--line);
	}

	.brand {
		display: flex;
		align-items: center;
		gap: 9px;
		font: 600 14px var(--sans);
	}

	.brand img {
		display: block;
	}

	p {
		flex: 1;
		margin: 0;
		color: var(--muted);
		font-size: 13px;
	}

	p a {
		color: var(--fg);
		text-decoration: underline;
		text-underline-offset: 3px;
	}

	p a:hover {
		color: #5d87ff;
	}

	.links {
		display: flex;
		gap: 20px;
	}

	.links a {
		display: flex;
		align-items: center;
		gap: 6px;
		color: var(--muted);
		font-size: 13px;
		text-decoration: none;
		transition: color 0.15s;
	}

	.links a:hover {
		color: var(--fg);
	}

	@media (max-width: 640px) {
		.footer {
			flex-wrap: wrap;
			gap: 12px 24px;
		}

		p {
			flex-basis: 100%;
			order: 3;
		}
	}
</style>
