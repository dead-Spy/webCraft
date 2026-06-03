<script>
    import { onMount } from "svelte";
    import gsap from "gsap";

    let gridRef = $state();
    let mouseGlowRef = $state();
    let contentGroup = $state();

    onMount(() => {
        gsap.fromTo(
            contentGroup.children,
            { opacity: 0, y: 30 },
            { opacity: 1, y: 0, duration: 1.2, stagger: 0.15, ease: "power4.out", delay: 0.2 }
        );

        gsap.set(gridRef, { opacity: 0 });
        gsap.to(gridRef, { opacity: 0.5, duration: 2, ease: "power2.out", delay: 0.5 });

        const glowX = gsap.quickTo(mouseGlowRef, "x", { duration: 0.6, ease: "power3.out" });
        const glowY = gsap.quickTo(mouseGlowRef, "y", { duration: 0.6, ease: "power3.out" });
        const gridX = gsap.quickTo(gridRef, "x", { duration: 1, ease: "power2.out" });
        const gridY = gsap.quickTo(gridRef, "y", { duration: 1, ease: "power2.out" });
        const contentX = gsap.quickTo(contentGroup, "x", { duration: 1.2, ease: "power2.out" });
        const contentY = gsap.quickTo(contentGroup, "y", { duration: 1.2, ease: "power2.out" });

        const handleInteraction = (e) => {
            const { clientX, clientY } = e;
            const { innerWidth, innerHeight } = window;

            glowX(clientX);
            glowY(clientY);

            const xPct = clientX / innerWidth - 0.5;
            const yPct = clientY / innerHeight - 0.5;

            gridX(-xPct * 30);
            gridY(-yPct * 30);
            contentX(xPct * 15);
            contentY(yPct * 10);
        };

        window.addEventListener("mousemove", handleInteraction);
        return () => window.removeEventListener("mousemove", handleInteraction);
    });
</script>

<section id="hero" class="relative flex h-screen w-full flex-col items-center justify-center overflow-hidden bg-[#050505] px-6 text-white md:px-8 font-sans select-none">
    <div
        bind:this={mouseGlowRef}
        class="pointer-events-none absolute left-0 top-0 z-0 h-[800px] w-[800px] -translate-x-1/2 -translate-y-1/2 rounded-full bg-[radial-gradient(circle,rgba(59,130,246,0.06)_0%,rgba(147,51,234,0.03)_40%,transparent_70%)] blur-3xl will-change-transform"
    ></div>

    <div
        bind:this={gridRef}
        class="pointer-events-none absolute inset-0 z-0 bg-[linear-gradient(to_right,rgba(255,255,255,0.04)_1px,transparent_1px),linear-gradient(to_bottom,rgba(255,255,255,0.04)_1px,transparent_1px)] bg-[size:4rem_4rem] [mask-image:radial-gradient(ellipse_60%_50%_at_50%_50%,#000_40%,transparent_100%)] will-change-transform"
    ></div>

    <div class="pointer-events-none absolute inset-0 z-10 bg-[radial-gradient(circle_at_center,rgba(5,5,5,0)_0%,#050505_100%)]"></div>

    <div bind:this={contentGroup} class="relative z-20 flex w-full max-w-5xl flex-col items-center gap-6 text-center md:gap-8 will-change-transform">
        <h1 class="font-serif text-[11vw] font-normal leading-[0.9] tracking-tight text-white md:text-[8vw] uppercase">
            Engineering Digital Dominance
        </h1>

        <p class="max-w-2xl text-base font-light leading-relaxed tracking-wide text-white/60 md:text-lg">
            A bespoke high-performance design and production studio run by a single engineer. Speed, absolute tactical precision, and zero communication overhead.
        </p>

        <div class="mt-4 flex flex-col sm:flex-row items-center gap-4 sm:gap-6">
            <a
                href="#work"
                class="group relative overflow-hidden rounded-full bg-white px-8 py-3.5 text-sm font-medium text-black transition-all duration-300 hover:scale-105 hover:shadow-[0_0_30px_rgba(255,255,255,0.2)]"
            >
                <span class="relative z-10">Selected Work</span>
                <div class="absolute inset-0 z-0 origin-left scale-x-0 bg-neutral-200 transition-transform duration-300 group-hover:scale-x-100"></div>
            </a>
            <a
                href="#stats"
                class="group flex items-center gap-2 rounded-full border border-white/10 bg-white/5 px-8 py-3.5 text-sm font-medium text-white/70 backdrop-blur-md transition-all duration-300 hover:bg-white/10 hover:text-white"
            >
                View Pricing
                <span class="text-blue-500 transition-transform duration-300 group-hover:translate-x-1">→</span>
            </a>
        </div>
    </div>
</section>