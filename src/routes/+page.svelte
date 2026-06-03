<script>
    import { 
        Seo, 
        Cursor, 
        Header, 
        Hero, 
        Manifesto, 
        Showcase, 
        WorksList, 
        Brands, 
        Stats, 
        Testimonials, 
        Faq, 
        Footer 
    } from "$lib";
</script>

<Seo />
<Cursor />
<Header />

<main class="relative w-full bg-[var(--color-bg-base)] text-[var(--color-text-primary)] transition-colors duration-400">
    <Hero />
    <Manifesto />
    <Showcase />
    <WorksList />
    <Brands />
    <Stats />
    <Testimonials />
    <Faq />
</main>

<Footer />