<script>
    import { onMount } from "svelte";
    import gsap from "gsap";
    import ScrollTrigger from "gsap/ScrollTrigger";

    const paragraph = "I believe exceptional products are built by focused engineers, not bloated agencies. No layers of communication, no overhead, no corporate friction. Just raw code, radical transparency, and high-performance engineering designed to push your business forward.";
    const words = paragraph.split(" ");

    let manifestoRef = $state();

    onMount(() => {
        gsap.registerPlugin(ScrollTrigger);

        const spans = manifestoRef.querySelectorAll(".word");

        const st = gsap.to(spans, {
            color: "#ffffff",
            stagger: 0.1,
            ease: "none",
            scrollTrigger: {
                trigger: manifestoRef,
                start: "top 85%",
                end: "bottom 50%",
                scrub: 1
            }
        });

        return () => {
            st.scrollTrigger?.kill();
            st.kill();
        };
    });
</script>

<section
    id="manifesto"
    class="relative flex w-full flex-col items-center justify-center border-t border-white/5 bg-[#050505] px-6 py-32 text-white md:px-24 md:py-48 select-none"
>
    <span class="mb-12 text-center font-mono text-[10px] uppercase tracking-[0.2em] text-white/40">
        The Protocol
    </span>

    <p
        bind:this={manifestoRef}
        class="flex w-full max-w-5xl flex-wrap justify-center gap-x-2.5 gap-y-1 text-center font-serif text-3xl md:gap-y-3 md:text-5xl lg:text-6xl"
    >
        {#each words as word}
            <span class="word pointer-events-none text-white/15 will-change-[color] transition-colors duration-300">
                {word}
            </span>
        {/each}
    </p>
</section>