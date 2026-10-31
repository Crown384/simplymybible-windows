<script lang="ts">
	import { resolve } from '$app/paths';
	import { SITE_NAME, SITE_URL, TWITTER_URL } from '#lib/config.js';
	import Doc from '#lib/Doc.svelte';

	const title = `Support | ${SITE_NAME}`;
	const description = 'Help with Bible for Windows, and how to reach out.';
	const url = `${SITE_URL}/support`;
</script>

<svelte:head>
	<title>{title}</title>
	<meta name="description" content={description} />
	<link rel="canonical" href={url} />
</svelte:head>

<Doc heading="Support" meta="Bible for Windows">
	<p class="lede">
		Have a question or running into an issue with the Windows build? Reach out directly to Stephen on
		<a href={TWITTER_URL} target="_blank" rel="noopener noreferrer">Twitter / X</a>.
	</p>

	<h2>System Requirements</h2>
	<p>
		Bible for Windows runs natively on Windows 10 and Windows 11 (64-bit). No installation or background services required — just run the executable.
	</p>

	<h2>Back up or export your notes</h2>
	<p>
		Inside the app, use <strong>Export as Markdown</strong> (Ctrl+E) or <strong>Export as JSON</strong> (Ctrl+Shift+E) under Notes and
		highlights. Your data is stored locally on your PC in a portable SQLite database.
	</p>

	<h2>Keyboard Shortcuts</h2>
	<p>
		Use <strong>Ctrl+K</strong> to quickly jump to any passage or reference, <strong>Ctrl+F</strong> to instant-search across all verses, and <strong>Shift+Ctrl+L</strong> to switch between Light, Sepia, and Dark themes.
	</p>

	<h2>Translations</h2>
	<p>
		The KJV, WEB, BSB, ASV, YLT, Darby, and Webster translations are built in and work completely offline.
	</p>

	<h2>Privacy</h2>
	<p>
		Bible collects no personal data and runs fully offline. See the
		<a href={resolve('/(site)/privacy')}>privacy policy</a> for details.
	</p>
</Doc>
