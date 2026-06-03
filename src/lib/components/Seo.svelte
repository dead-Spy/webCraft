<script>
    let {
        title = "WebCraft — High-Performance Digital Studio",
        description = "Bespoke digital engineering and premium web experiences crafted by Tanvir Amin. Specializing in Svelte, Next.js, and complex hardware-accelerated motion.",
        url = "https://tanviramin.is-a.dev",
        image = "/og-image.png"
    } = $props();
</script>

<svelte:head>
    <title>{title}</title>
    <meta name="title" content={title} />
    <meta name="description" content={description} />
    <meta name="robots" content="index, follow" />
    <meta name="theme-color" content="#050505" />
    <meta name="author" content="Tanvir Amin" />

    <meta property="og:type" content="website" />
    <meta property="og:url" content={url} />
    <meta property="og:title" content={title} />
    <meta property="og:description" content={description} />
    <meta property="og:image" content={image} />

    <meta property="twitter:card" content="summary_large_image" />
    <meta property="twitter:url" content={url} />
    <meta property="twitter:title" content={title} />
    <meta property="twitter:description" content={description} />
    <meta property="twitter:image" content={image} />
</svelte:head>