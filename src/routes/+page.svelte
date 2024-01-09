<script>
	const json_ld = {
		'@context': 'http://schema.org',
		'@type': 'Organization',
		name: 'Your Organization Name',
		url: 'https://yourorganization.com',
		logo: 'https://yourorganization.com/logo.png',
	};
</script>

<svelte:head>
	<svelte:element this="script" type="application/ld+json">
		{@html JSON.stringify(json_ld)}
	</svelte:element>
</svelte:head>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
