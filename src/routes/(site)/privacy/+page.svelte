<script lang="ts">
	import { resolve } from '$app/paths';
	import { SITE_NAME, SITE_URL } from '#lib/config.js';
	import Doc from '#lib/Doc.svelte';

	const title = `Privacy policy | ${SITE_NAME}`;
	const description =
		'The Bible app collects no data: no account, no analytics, no ads, no tracking. Your highlights, notes and bookmarks stay on your computer.';
	const url = `${SITE_URL}/privacy`;
</script>

<svelte:head>
	<title>{title}</title>
	<meta name="description" content={description} />
	<link rel="canonical" href={url} />
</svelte:head>

<Doc heading="Privacy policy" meta="Updated October 2026. Covers Bible for Windows, and this website.">
	<p class="lede">
		The Bible app collects no data. There's no account, no analytics, no ads and no tracking. Your
		highlights, notes, bookmarks, searches and reading history are never sent to anyone.
	</p>

	<h2>What stays on your computer</h2>
	<p>
		The app saves your highlights, notes, bookmarks, reading position, history and settings in a
		local file on your Windows PC. They leave your computer only when you export or share them.
		Translations you import stay entirely local.
	</p>

	<h2>When the app uses the internet</h2>
	<p>
		By default, never. The seven built-in translations are inside the app, and it makes no network
		connections for reading.
	</p>
	<p>The app only connects to the internet if you explicitly configure online translations:</p>
	<ul>
		<li>
			Online translations you add yourself (such as the ESV, NLT, NET, or a Bible from API.Bible).
			The app connects directly to the respective publisher server using your API key.
		</li>
	</ul>

	<h2>Sharing and export</h2>
	<p>
		When you copy a verse or export your notes to Markdown or JSON, it is saved directly to your computer.
	</p>

	<h2>This website</h2>
	<p>
		This website sets no tracking cookies and serves its own fonts. It uses minimal privacy-preserving
		Vercel Web Analytics to measure overall site traffic without collecting personal data or linking visits to IP addresses.
	</p>

	<h2>Changes and questions</h2>
	<p>
		Changes to this policy will be posted on this page. Questions are welcome on our
		<a href={resolve('/(site)/support')}>support page</a>.
	</p>
</Doc>
