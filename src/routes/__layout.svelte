<script lang="typescript">
	import { Header, Content, Footer } from "$lib/Site";
	import { BRAND_ASSETS } from "$config";
</script>

<svelte:head>
	<!-- Favicon -->
	<link rel="icon" type="image/svg+xml" href={BRAND_ASSETS.favicon}>

	<!-- Fonts -->
	<link rel="preload" as="font" type="font/woff2" href={BRAND_ASSETS.fonts.sansSerif} crossorigin="anonymous">
	<link rel="preload" as="font" type="font/woff2" href={BRAND_ASSETS.fonts.serif} crossorigin="anonymous">
</svelte:head>

<Header />
<Content><slot /></Content>
<Footer />

<style lang="postcss">
	@import "$styles/global.css";

	/*
		FIXME:
		For some reason, while building process (`npm run build`),
		custom-media queries defined in `global.css`
		are ignored in compiling Svelte components.
		They work only inside the global.css file (along with imports).
		Meanwhile, in the dev process (`npm run dev`), it works. 🤯
		Intended or bug?
	*/
	@custom-media --motion (prefers-reduced-motion: no-preference);
	@custom-media --no-motion (prefers-reduced-motion: reduce);

	:global(#svelte) {
		--header-height: 5em;

		--content-padding: min(2.5vw, 1em);

		position: relative;

		display: grid;
		grid-template-areas:
			"header"
			"content"
			"footer";
		grid-template-rows:
			var(--header-height)
			calc(100% - var(--header-height))
			auto;
		grid-template-columns: 100vw;
	}
</style>
