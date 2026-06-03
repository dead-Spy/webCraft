<script>
    import { onMount } from "svelte";
    import gsap from "gsap";

    let trackRef = $state();

    onMount(() => {
        const ctx = gsap.context(() => {
            gsap.to(trackRef, {
                xPercent: -50,
                repeat: -1,
                duration: 20,
                ease: "none"
            });
        });

        return () => ctx.revert();
    });

    const technologies = [
        "REACT",
        "NEXT.JS",
        "TAILWIND CSS",
        "SVELTE",
        "LARAVEL",
        "GSAP",
        "NODE.JS",
        "HIGH PERFORMANCE"
    ];
</script>

<section class="relative z-10 flex w-full flex-col items-center justify-center overflow-hidden border-t border-white/5 bg-[#050505] py-16 md:py-24 select-none">
    <div class="pointer-events-none absolute inset-y-0 left-0 z-10 w-32 bg-gradient-to-r from-[#050505] to-transparent md:w-80"></div>
    <div class="pointer-events-none absolute inset-y-0 right-0 z-10 w-32 bg-gradient-to-l from-[#050505] to-transparent md:w-80"></div>

    <p class="relative z-20 mb-10 text-center font-mono text-[10px] uppercase tracking-[0.3em] text-white/30">
        Core Technical Arsenal
    </p>

    <div class="relative z-0 flex w-full overflow-hidden">
        <div bind:this={trackRef} class="flex whitespace-nowrap will-change-transform">
            <div class="flex items-center gap-16 px-8 md:gap-32 md:px-16">
                {#each technologies as tech}
                    <div class="flex items-center gap-16 font-mono text-xl font-medium tracking-wider text-white/20 transition-colors duration-500 hover:text-blue-500 md:gap-32 md:text-3xl cursor-default">
                        <span>{tech}</span>
                        <span class="font-serif text-lg font-light text-white/5 md:text-2xl">//</span>
                    </div>
                {/each}
            </div>

            <div class="flex items-center gap-16 px-8 md:gap-32 md:px-16" aria-hidden="true">
                {#each technologies as tech}
                    <div class="flex items-center gap-16 font-mono text-xl font-medium tracking-wider text-white/20 transition-colors duration-500 hover:text-blue-500 md:gap-32 md:text-3xl cursor-default">
                        <span>{tech}</span>
                        <span class="font-serif text-lg font-light text-white/5 md:text-2xl">//</span>
                    </div>
                {/each}
            </div>
        </div>
    </div>
</section>