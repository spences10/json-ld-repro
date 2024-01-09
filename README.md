# JSON-LD script issue

With this reproduction of an issue I'm facing with (what I believe is)
SvelteKit.

I want to have a JSON-LD script in the head of my page. I'm using the
`<svelte:head>` and `<svelte:element>` tags to do this. Basic example
in the [`src/routes/+page.svelte`](./src/routes/+page.svelte) file.

```svelte
<script>
	const json_ld = {
		'@context': 'http://schema.org',
		'@type': 'Organization',
		name: 'Your Organization Name',
		url: 'https://yourorganization.com',
		logo: 'https://yourorganization.com/logo.png'
	};
</script>

<svelte:head>
	<svelte:element this="script" type="application/ld+json">
		{@html JSON.stringify(json_ld)}
	</svelte:element>
</svelte:head>

<h1>Welcome to SvelteKit</h1>
<p>
	Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the
	documentation
</p>
```

However, when I run `npm run dev` and visit the page, I get the
following output for the head:

```html
<head>
	<meta charset="utf-8" />
	<link rel="icon" href="./favicon.png" />
	<meta
		name="viewport"
		content="width=device-width, initial-scale=1"
	/>
	<!--ssr:0-->
	<!--ssr:1-->
	<script type="application/ld+json">
		<!--ssr:2--><!--ssr:3-->{"@context":"http://schema.org","@type":"Organization","name":"Your Organization Name","url":"https://yourorganization.com","logo":"https://yourorganization.com/logo.png"}<!--ssr:3--><!--ssr:2-->
	</script>
	<!--ssr:1-->
	<!--ssr:0-->
</head>
```

The `<!--ssr:*-->` tags inside the `ld+json` script tag mean the
output cannot be parsed.

I have tried both `vitePreprocess` and `svelte-preprocess` with the
`preserve` option set to `['ld+json']` but neither seem to work.

```js
preprocess: vitePreprocess({
  preserve: ['ld+json']
}),
```
