<script lang="ts">
	import { resolve } from '$app/paths';
	import Footer from '#lib/Footer.svelte';
	import Nav from '#lib/Nav.svelte';
	import CompareCard from '#lib/cards/CompareCard.svelte';
	import JumpCard from '#lib/cards/JumpCard.svelte';
	import SearchCard from '#lib/cards/SearchCard.svelte';
	import StudyCard from '#lib/cards/StudyCard.svelte';
	import ThemesCard from '#lib/cards/ThemesCard.svelte';
	import TypesetCard from '#lib/cards/TypesetCard.svelte';
	import { NAME, SITE_NAME, SITE_URL, VERSION, WINDOWS_ARCH, WINDOWS_SIZE } from '#lib/config.js';
	import Showcase from '#lib/demo/Showcase.svelte';
	import { Player } from '#lib/demo/player.svelte.js';
	import { play } from '#lib/demo/sound.js';
	import { reducedMotion, reveal } from '#lib/motion.svelte.js';

	const title = `${NAME}: a fast, native reader for Windows | ${SITE_NAME}`;
	const description =
		'A very fast, native Bible reader for Windows. Beautifully typeset, searchable as you type, with highlights, notes and bookmarks kept on your computer.';
	const url = `${SITE_URL}/`;
	const image = `${SITE_URL}/og.jpg`;
	const imageAlt = `The ${NAME} app icon and name beside the reader open at John 1`;

	const app = JSON.stringify({
		'@context': 'https://schema.org',
		'@type': 'SoftwareApplication',
		name: NAME,
		description,
		url,
		image,
		operatingSystem: 'Windows 10, Windows 11',
		applicationCategory: 'ReferenceApplication',
		offers: { '@type': 'Offer', price: '0', priceCurrency: 'USD' },
		downloadUrl: `${SITE_URL}/download`,
		softwareVersion: VERSION
	}).replaceAll('<', '\\u003c');
	const jsonLd = `<script type="application/ld+json">${app}<\\/script>`;

	const player = new Player();

	let paused: Record<string, boolean> = $state({});

	const reading = [
		{
			title: 'Typeset for reading',
			body: 'Literata at a comfortable measure, with superscript verse numbers, poetry that keeps its lines, LORD in small capitals and the words of Christ in red. Paragraphs or a verse per line.',
			Visual: TypesetCard
		},
		{
			title: 'Light, sepia and dark',
			body: 'Three themes made for long reading, from white paper to warm sepia to a soft dark. Shift+Ctrl+L switches between them, and the size, spacing and measure are yours to set.',
			Visual: ThemesCard
		}
	];

	const study = [
		{
			title: 'Jump anywhere',
			body: 'Press Ctrl+K and type a reference the way you’d write it: jn 3:16, Rom 8, 1co13, even revalation 21. Recent places, translations and commands come up too.',
			Visual: JumpCard
		},
		{
			title: 'Search as you type',
			body: 'Every verse is searched as you type, in under 2 ms. Quote a phrase, put a minus before a word to leave it out, and search the whole Bible, one testament or one book.',
			Visual: SearchCard
		},
		{
			title: 'Highlights and notes',
			body: 'Highlight in six colours, write notes in the margin, bookmark verses and follow a reading plan. It all stays in a file on your PC, and exports to Markdown or JSON.',
			Visual: StudyCard
		},
		{
			title: 'Translations side by side',
			body: 'Seven public-domain translations are built in. Read them in parallel columns, or compare one verse across all of them. Add the NLT and NET free, the ESV with a free key, or import a file you own.',
			Visual: CompareCard
		}
	];

	const shortcuts = [
		{ keys: ['Ctrl', 'K'], label: 'Jump to a passage', primary: true },
		{ keys: ['Ctrl', 'F'], label: 'Search' },
		{ keys: ['←', '→'], label: 'Previous or next chapter' },
		{ keys: ['Ctrl+[', 'Ctrl+]'], label: 'Back and forward' },
		{ keys: ['J', 'K'], label: 'Move between verses' },
		{ keys: ['1–6'], label: 'Highlight in a colour' },
		{ keys: ['N'], label: 'Write a note' },
		{ keys: ['C'], label: 'Compare translations' },
		{ keys: ['Shift', 'Ctrl', 'P'], label: 'Read in parallel' },
		{ keys: ['Shift', 'Ctrl', 'L'], label: 'Change theme' }
	];
</script>

<svelte:head>
	<title>{title}</title>
	<meta name="description" content={description} />
	<link rel="canonical" href={url} />
	<meta property="og:type" content="website" />
	<meta property="og:site_name" content={SITE_NAME} />
	<meta property="og:locale" content="en_US" />
	<meta property="og:url" content={url} />
	<meta property="og:title" content={title} />
	<meta property="og:description" content={description} />
	<meta property="og:image" content={image} />
	<meta property="og:image:type" content="image/jpeg" />
	<meta property="og:image:width" content="1200" />
	<meta property="og:image:height" content="630" />
	<meta property="og:image:alt" content={imageAlt} />
	<meta name="twitter:card" content="summary_large_image" />
	<meta name="twitter:title" content={title} />
	<meta name="twitter:description" content={description} />
	<meta name="twitter:image" content={image} />
	<meta name="twitter:image:alt" content={imageAlt} />
	<!-- eslint-disable-next-line svelte/no-at-html-tags -->
	{@html jsonLd}
</svelte:head>

{#snippet windows()}
	<svg viewBox="0 0 16 16" width="16" height="16" fill="currentColor" aria-hidden="true">
		<path d="M0 2.29 6.55 1.4v6.07H0V2.29zm7.45-1.52L16 0v7.47H7.45V.77zM0 8.53h6.55v6.08L0 13.71V8.53zm7.45 0H16V16l-8.55-1.22V8.53z"/>
	</svg>
{/snippet}

{#snippet actions()}
	<div class="actions">
		<a class="download" href={resolve('/download')} data-sveltekit-reload>
			{@render windows()}
			Download for Windows
		</a>
		<a class="web" href={resolve('/read')} data-sveltekit-reload>
			<svg viewBox="0 0 16 16" aria-hidden="true">
				<circle cx="8" cy="8" r="6.5" />
				<path d="M1.5 8h13M8 1.5c-1.8 1.7-2.8 4-2.8 6.5s1 4.8 2.8 6.5M8 1.5c1.8 1.7 2.8 4 2.8 6.5s-1 4.8-2.8 6.5" />
			</svg>
			Read online
		</a>
	</div>
{/snippet}

{#snippet card(item: (typeof reading)[number], i: number)}
	<article class="card" style:--delay="{i * 90}ms" {@attach reveal}>
		<item.Visual paused={paused[item.title]} />
		<div class="caption">
			<div class="heading">
				<h3>{item.title}</h3>
				{#if !reducedMotion.current}
					<button
						type="button"
						class="pause"
						aria-label="{paused[item.title] ? 'Play' : 'Pause'} the {item.title} animation"
						onclick={() => (paused[item.title] = !paused[item.title])}
					>
						{#if paused[item.title]}
							<svg viewBox="0 0 16 16" aria-hidden="true"><path d="M5 3.2v9.6L12.6 8z" /></svg>
						{:else}
							<svg viewBox="0 0 16 16" aria-hidden="true"><path d="M4.5 3h2.4v10H4.5zM9.1 3h2.4v10H9.1z" /></svg>
						{/if}
					</button>
				{/if}
			</div>
			<p>{item.body}</p>
		</div>
	</article>
{/snippet}

<Nav ontoggle={() => player.sound && play('switch')} />

<main id="top">
	<header class="hero">
		<img class="logo" src="/icon.png" width="112" height="112" alt="" />
		<h1>The Bible, instantly.</h1>
		<p class="lede">
			A very fast, native Bible reader for Windows, written in Rust.<br />
			Type a reference, press Return, and the passage is already there.
		</p>
		<div class="cta">
			{@render actions()}
			<p class="meta">
				Free · Version {VERSION} · {WINDOWS_ARCH} · {WINDOWS_SIZE}
			</p>
		</div>
	</header>

	<section class="showcase" aria-label="Demo">
		<Showcase {player} />
	</section>

	<div id="features">
		<section class="section" aria-labelledby="reading-title">
			<h2 id="reading-title" {@attach reveal}>Reading</h2>
			<div class="cards">
				{#each reading as item, i (item.title)}
					{@render card(item, i)}
				{/each}
			</div>
		</section>

		<section class="section" aria-labelledby="study-title">
			<h2 id="study-title" {@attach reveal}>Built for study</h2>
			<div class="cards">
				{#each study as item, i (item.title)}
					{@render card(item, i % 2)}
				{/each}
			</div>
		</section>
	</div>

	<section id="shortcuts" class="section split" aria-labelledby="shortcuts-title">
		<div class="intro" {@attach reveal}>
			<h2 id="shortcuts-title">Shortcuts</h2>
			<p>Every action has a key, and most can be changed in Settings. Ctrl+/ lists them all.</p>
		</div>
		<ul class="shortcuts" {@attach reveal}>
			{#each shortcuts as shortcut (shortcut.label)}
				<li>
					<span class="keys">
						{#each shortcut.keys as key (key)}
							<kbd class={{ primary: shortcut.primary }}>{key}</kbd>
						{/each}
					</span>
					<span class="label">{shortcut.label}</span>
				</li>
			{/each}
		</ul>
	</section>

	<section id="install" class="section" aria-labelledby="install-title">
		<div class="intro" {@attach reveal}>
			<h2 id="install-title">Install</h2>
			<p>Free for {WINDOWS_ARCH}, or in your browser.</p>
			{@render actions()}
		</div>
	</section>
</main>

<Footer>Scripture on this page is from the KJV, WEB and BSB, which are in the public domain.</Footer>

<style>
	.hero {
		display: flex;
		flex-direction: column;
		align-items: center;
		max-width: 900px;
		margin: 0 auto;
		padding: 72px 24px 48px;
		text-align: center;
	}

	.hero > * {
		animation: rise 0.9s cubic-bezier(0.2, 0.7, 0.2, 1) both;
	}

	.hero > :nth-child(2) {
		animation-delay: 0.08s;
	}

	.hero > :nth-child(3) {
		animation-delay: 0.16s;
	}

	.hero > :nth-child(4) {
		animation-delay: 0.24s;
	}

	.logo {
		display: block;
		filter: drop-shadow(0 18px 40px rgba(0, 0, 0, 0.55)) drop-shadow(0 0 40px rgba(110, 140, 255, 0.14));
		animation-name: pop;
	}

	:global(:root[data-theme='light']) .logo {
		filter: drop-shadow(0 18px 32px rgba(0, 0, 0, 0.2)) drop-shadow(0 0 40px rgba(110, 140, 255, 0.1));
	}

	h1 {
		margin: 32px 0 0;
		font: 700 58px/1.05 var(--display);
		letter-spacing: -0.035em;
		text-wrap: balance;
	}

	.lede {
		max-width: 580px;
		margin: 20px 0 0;
		color: var(--muted);
		font-size: 18px;
		line-height: 29px;
		text-wrap: pretty;
	}

	.cta {
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 16px;
		margin-top: 32px;
	}

	.actions {
		--solid-edge: 0 10px 30px rgba(255, 255, 255, 0.07);
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
		gap: 12px;
	}

	:global(:root[data-theme='light']) .actions {
		--solid-edge: 0 10px 30px rgba(0, 0, 0, 0.14);
	}

	.download {
		--fill: var(--solid);
		--fill-hover: var(--solid-hover);
		--ink: var(--on-solid);
		--edge: var(--solid-edge);
	}

	.web {
		--fill: var(--raised);
		--fill-hover: var(--raised), color-mix(in srgb, var(--fg) 8%, transparent);
		--ink: var(--fg);
		--edge: var(--raised-edge);
	}

	.download,
	.web {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		gap: 9px;
		padding: 13px 22px 13px 20px;
		border-radius: 999px;
		background: var(--fill);
		box-shadow: var(--edge);
		color: var(--ink);
		font: 600 15px/18px var(--sans);
		text-decoration: none;
		transition:
			scale 0.2s,
			background-color 0.2s;
	}

	.download:hover,
	.web:hover {
		background: var(--fill-hover);
		scale: 1.03;
	}

	.download svg,
	.web svg {
		width: 15px;
		height: 18px;
		fill: currentColor;
	}

	.meta {
		margin: 0;
		color: var(--muted);
		font-size: 12.5px;
		letter-spacing: -0.01em;
	}

	.showcase {
		max-width: 1100px;
		margin: 0 auto;
		padding: 0 24px 32px;
	}

	.section {
		max-width: 1080px;
		margin: 0 auto;
		padding: 72px 24px;
	}

	h2 {
		margin: 0;
		font: 700 36px/1.15 var(--display);
		letter-spacing: -0.025em;
	}

	.cards {
		display: grid;
		grid-template-columns: repeat(2, minmax(0, 1fr));
		gap: 20px;
		margin-top: 28px;
	}

	.card {
		overflow: hidden;
		border-radius: 20px;
		background: var(--surface);
		box-shadow: var(--edge);
		transition: box-shadow 0.2s;
	}

	.caption {
		padding: 24px 28px 28px;
	}

	.heading {
		display: flex;
		align-items: baseline;
		justify-content: space-between;
		gap: 12px;
	}

	h3 {
		margin: 0;
		font: 600 20px/1.3 var(--sans);
		letter-spacing: -0.02em;
	}

	.pause {
		display: grid;
		place-items: center;
		width: 26px;
		height: 26px;
		padding: 0;
		border: 0;
		border-radius: 999px;
		background: var(--raised);
		color: var(--muted);
		cursor: pointer;
		opacity: 0.6;
		transition:
			opacity 0.15s,
			background-color 0.15s,
			color 0.15s;
	}

	.pause:hover {
		opacity: 1;
		background: var(--fg);
		color: var(--bg);
	}

	.pause svg {
		width: 12px;
		height: 12px;
		fill: currentColor;
	}

	.caption p {
		margin: 10px 0 0;
		color: var(--muted);
		font-size: 15px;
		line-height: 24px;
		text-wrap: pretty;
	}

	.split {
		display: grid;
		grid-template-columns: 1fr 1.3fr;
		gap: 48px;
		align-items: start;
	}

	.intro p {
		max-width: 420px;
		margin: 16px 0 0;
		color: var(--muted);
		font-size: 16px;
		line-height: 26px;
	}

	#install .intro {
		display: flex;
		flex-direction: column;
		align-items: center;
		text-align: center;
		max-width: 540px;
		margin: 0 auto;
	}

	#install .actions {
		margin-top: 28px;
	}

	.shortcuts {
		display: flex;
		flex-direction: column;
		gap: 10px;
		margin: 0;
		padding: 0;
		list-style: none;
	}

	.shortcuts li {
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: 16px;
		padding: 10px 14px;
		border-radius: 12px;
		background: var(--surface);
		box-shadow: var(--edge);
	}

	.keys {
		display: flex;
		gap: 5px;
	}

	kbd {
		display: inline-grid;
		place-items: center;
		min-width: 26px;
		height: 26px;
		padding: 0 7px;
		border-radius: 6px;
		background: var(--raised);
		box-shadow: var(--raised-edge);
		color: var(--muted);
		font: 500 12.5px var(--sans);
	}

	kbd.primary {
		color: var(--fg);
	}

	.shortcuts .label {
		color: var(--fg);
		font-size: 14.5px;
	}

	@media (max-width: 840px) {
		.cards {
			grid-template-columns: 1fr;
		}

		.split {
			grid-template-columns: 1fr;
			gap: 32px;
		}

		h1 {
			font-size: 44px;
		}
	}
</style>
