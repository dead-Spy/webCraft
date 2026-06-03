<script>
    import { onMount } from "svelte";
    import gsap from "gsap";
    import ScrollTrigger from "gsap/ScrollTrigger";

    const services = [
        {
            title: "Architecture & Design",
            desc: "Crafting pixel-perfect user interfaces, custom motion mechanics, and deeply engaging user experiences that set elite industry standards.",
            icon: "M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"
        },
        {
            title: "Full-Stack Engineering",
            desc: "Architecting scalable backend structures, secure database layers, and zero-latency custom API integrations optimized for flawless performance.",
            icon: "M13 10V3L4 14h7v8l9-11h-7z"
        },
        {
            title: "Strategy & Deployment",
            desc: "Maximizing potential with advanced cloud deployment topologies, rigorous performance optimization, and meticulous technical SEO architecture.",
            icon: "M15 12a3 3 0 11-6 0 3 3 0 016 0z M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"
        }
    ];

    let gridRef = $state();

    onMount(() => {
        gsap.registerPlugin(ScrollTrigger);

        const cards = gridRef.querySelectorAll(".service-grid-card");

        const st = gsap.fromTo(
            cards,
            { y: 40, autoAlpha: 0 },
            {
                y: 0,
                autoAlpha: 1,
                duration: 1,
                stagger: 0.12,
                ease: "power3.out",
                scrollTrigger: {
                    trigger: gridRef,
                    start: "top 85%"
                }
            }
        );

        return () => {
            st.scrollTrigger?.kill();
            st.kill();
        };
    });
</script>

<section
    id="services"
    class="relative z-10 w-full overflow-hidden border-t border-white/5 bg-[#050505] py-32 text-white md:py-48"
>
    <div class="pointer-events-none absolute top-1/2 left-1/2 h-[800px] w-[800px] -translate-x-1/2 -translate-y-1/2 rounded-full bg-blue-600/[0.02] blur-[200px]"></div>

    <div class="mx-auto max-w-[1400px] px-6 md:px-12 flex flex-col items-center">
        <span class="mb-16 text-center font-mono text-[10px] uppercase tracking-[0.3em] text-white/40">
            Capabilities
        </span>

        <div
            bind:this={gridRef}
            class="grid w-full grid-cols-1 gap-6 md:gap-8 lg:grid-cols-3"
        >
            {#each services as service, i}
                <div class="service-grid-card group relative h-[50vh] w-full cursor-default overflow-hidden rounded-3xl border border-white/10 bg-[#0a0a0a] transition-colors duration-500 md:h-[65vh] lg:h-[75vh]">
                    <div class="absolute inset-0 z-10 bg-gradient-to-t from-black via-black/30 to-transparent"></div>

                    <div class="pointer-events-none absolute -top-32 -left-32 z-0 h-96 w-96 rounded-full bg-blue-600/0 opacity-0 transition-all duration-700 blur-[100px] group-hover:bg-blue-600/10 group-hover:opacity-100"></div>

                    <div class="absolute top-8 left-8 z-20 font-serif text-6xl text-white/5 transition-colors duration-500 group-hover:text-white/10">
                        0{i + 1}
                    </div>

                    <div class="absolute top-8 right-8 z-20 text-white/20 transition-all duration-500 group-hover:scale-110 group-hover:text-blue-500">
                        <svg class="h-7 w-7" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d={service.icon} />
                        </svg>
                    </div>

                    <div class="absolute bottom-8 left-8 right-8 z-20 flex flex-col gap-4 transition-transform duration-500 transform-gpu lg:gap-6 lg:group-hover:-translate-y-4">
                        <h3 class="font-serif text-2xl leading-tight tracking-tight text-white md:text-3xl lg:text-4xl">
                            {service.title}
                        </h3>

                        <div class="h-px w-full origin-left scale-x-100 bg-white/10 transition-transform duration-500 ease-out lg:scale-x-0 lg:group-hover:scale-x-100 lg:bg-white/20"></div>

                        <p class="font-sans text-sm leading-relaxed text-white/50 opacity-100 transition-opacity duration-500 ease-out lg:opacity-0 lg:group-hover:opacity-100">
                            {service.desc}
                        </p>
                    </div>
                </div>
            {/each}
        </div>
    </div>
</section>