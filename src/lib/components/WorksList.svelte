<script>
    import { onMount } from "svelte";
    import gsap from "gsap";

    const works = [
        {
            id: "01",
            name: "Shikor Platform",
            category: "Enterprise Real Estate Ecosystem",
            tech: "Laravel • React • Tailwind v4",
            metrics: "+140% Conversion Growth",
            year: "2026",
            image: "https://images.unsplash.com/photo-1600585154340-be6161a56a0c?auto=format&fit=crop&w=800&q=80"
        },
        {
            id: "02",
            name: "Cosmic Capsule",
            category: "3D Satellite Intelligence UI",
            tech: "Next.js • Three.js • GSAP",
            metrics: "Zero-Latency Solar Tracking",
            year: "2026",
            image: "https://images.unsplash.com/photo-1451187580459-43490279c0fa?auto=format&fit=crop&w=800&q=80"
        },
        {
            id: "03",
            name: "Imagery Studio",
            category: "Event Management Web Application",
            tech: "Vue.js • Node.js • Vanilla JS",
            metrics: "45% Reduction in Friction",
            year: "2026",
            image: "https://images.unsplash.com/photo-1540575467063-178a50c2df87?auto=format&fit=crop&w=800&q=80"
        }
    ];

    let containerRef = $state();
    let previewRef = $state();
    let previewImgRef = $state();

    onMount(() => {
        let mm = gsap.matchMedia();

        mm.add("(min-width: 1024px)", () => {
            const setX = gsap.quickTo(previewRef, "x", { duration: 0.4, ease: "power3.out" });
            const setY = gsap.quickTo(previewRef, "y", { duration: 0.4, ease: "power3.out" });

            const handleMouseMove = (e) => {
                const bounds = containerRef.getBoundingClientRect();
                setX(e.clientX - bounds.left);
                setY(e.clientY - bounds.top);
            };

            containerRef.addEventListener("mousemove", handleMouseMove);
            return () => containerRef.removeEventListener("mousemove", handleMouseMove);
        });

        return () => mm.revert();
    });

    function handleMouseEnter(imgSrc) {
        if (window.innerWidth < 1024) return;
        previewImgRef.src = imgSrc;
        gsap.to(previewRef, { autoAlpha: 1, scale: 1, duration: 0.3, ease: "power2.out" });
    }

    function handleMouseLeave() {
        if (window.innerWidth < 1024) return;
        gsap.to(previewRef, { autoAlpha: 0, scale: 0.8, duration: 0.3, ease: "power2.in" });
    }
</script>

<section
    id="work"
    class="w-full bg-[#050505] text-white py-32 border-t border-white/10 min-h-screen select-none relative"
>
    <div class="px-6 md:px-24 mb-24 max-w-7xl mx-auto flex flex-col md:flex-row justify-between items-end gap-6">
        <h2 class="text-5xl md:text-8xl font-serif tracking-tight leading-none">
            Selected<br /><span class="italic text-white/40">Works.</span>
        </h2>
        <p class="text-white/50 font-sans max-w-sm text-base md:text-lg leading-relaxed pb-2">
            A curation of production-ready architecture and full-stack solutions. Built for maximum business impact.
        </p>
    </div>

    <div bind:this={containerRef} class="px-6 md:px-24 max-w-7xl mx-auto flex flex-col relative">
        <div
            bind:this={previewRef}
            class="pointer-events-none absolute top-0 left-0 w-80 h-48 rounded-2xl overflow-hidden invisible opacity-0 z-40 shadow-2xl border border-white/20 -translate-x-1/2 -translate-y-1/2 hidden lg:block"
        >
            <img
                bind:this={previewImgRef}
                src=""
                alt="Project Preview"
                class="w-full h-full object-cover will-change-transform"
            />
        </div>

        <div class="flex border-b border-white/20 pb-4 mb-4 text-[10px] font-mono text-white/40 uppercase tracking-[0.2em] px-4">
            <div class="w-12">ID</div>
            <div class="flex-1">Project</div>
            <div class="hidden md:block w-1/4">Stack</div>
            <div class="hidden lg:block w-1/4">Impact</div>
            <div class="w-16 text-right">Year</div>
        </div>

        {#each works as work}
            <div
                onmouseenter={() => handleMouseEnter(work.image)}
                onmouseleave={handleMouseLeave}
                class="group flex items-center border-b border-white/10 py-8 md:py-12 px-4 hover:bg-white/[0.02] transition-colors duration-500 cursor-default relative overflow-hidden"
            >
                <div class="w-12 text-sm font-mono text-white/30 group-hover:text-white/80 transition-colors z-10">
                    {work.id}
                </div>
                <div class="flex-1 z-10">
                    <h3 class="text-2xl md:text-5xl font-serif text-white/60 group-hover:text-white lg:group-hover:translate-x-4 transition-all duration-500 transform-gpu">
                        {work.name}
                    </h3>
                    <span class="block md:hidden text-xs font-mono text-blue-500 mt-2">{work.category}</span>
                </div>
                <div class="hidden md:block w-1/4 text-sm font-mono text-white/40 group-hover:text-white/80 transition-colors z-10">
                    {work.tech}
                </div>
                <div class="hidden lg:block w-1/4 text-sm font-sans font-medium text-blue-500 tracking-wide z-10">
                    {work.metrics}
                </div>
                <div class="w-16 text-right text-sm font-mono text-white/40 group-hover:text-white/90 transition-colors z-10">
                    {work.year}
                </div>
            </div>
        {/each}

        <div class="mt-20 flex justify-center w-full">
            <a
                href="https://tanviramin.is-a.dev"
                target="_blank"
                rel="noreferrer"
                class="px-8 py-3.5 rounded-full border border-white/10 bg-white/5 text-white/80 hover:bg-white hover:text-black transition-all duration-300 font-sans text-sm font-medium inline-block shadow-lg hover:scale-105"
            >
                View Production Archives
            </a>
        </div>
    </div>
</section>