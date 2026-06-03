<script>
    import Plus from "@lucide/svelte/icons/plus";
    import { slide } from "svelte/transition";

    const faqs = [
        {
            q: "How can a solo engineer deliver agency-scale platforms?",
            a: "By eliminating project managers, account executives, and corporate overhead. You collaborate directly with the engineer building the core system, resulting in faster development cycles, absolute architectural clarity, and zero loss in translation."
        },
        {
            q: "What technologies power your production apps?",
            a: "The stack is optimized for speed and long-term maintainability. I architect systems using Svelte, Next.js, and React for high-performance interactive user interfaces, combined with robust Laravel and Node.js backend infrastructure."
        },
        {
            q: "What does your typical development timeline look like?",
            a: "Production-ready landing pages and sleek portfolios are typically delivered within 2 weeks. Complex full-stack web applications, custom enterprise platforms, or deep 3D interfaces generally span between 4 to 8 weeks."
        },
        {
            q: "How do you handle post-launch scaling and infrastructure?",
            a: "Every application is built on modern serverless or optimized cloud topologies designed to scale seamlessly with minimal maintenance. Complete technical documentation and a structured handoff are provided for seamless evolution."
        }
    ];

    let activeIndex = $state(null);

    function toggle(index) {
        activeIndex = activeIndex === index ? null : index;
    }
</script>

<section
    id="faq"
    class="relative z-10 w-full overflow-hidden border-t border-white/10 bg-[#050505] py-32 text-white select-none"
>
    <div class="pointer-events-none absolute top-0 right-0 h-[500px] w-[500px] rounded-full bg-blue-600/[0.03] blur-[150px]"></div>

    <div class="mx-auto flex max-w-7xl flex-col gap-16 px-6 md:flex-row md:px-24">
        <div class="w-full md:w-1/3">
            <span class="mb-6 block font-mono text-xs uppercase tracking-[0.2em] text-white/40">
                FAQ
            </span>
            <h2 class="font-serif text-4xl leading-tight md:text-5xl">
                Frequently<br />
                <span class="italic text-white/40">Asked</span>
            </h2>
            <p class="mt-6 font-sans text-base font-light leading-relaxed text-white/50">
                Clear answers regarding the operational execution, development workflow, and technology choices.
            </p>

            <a
                href="#contact"
                class="group mt-8 inline-flex items-center gap-4 font-mono text-[11px] uppercase tracking-wider text-white/70 transition-colors hover:text-white"
            >
                Still have questions?
                <span class="h-px w-8 origin-left scale-x-100 bg-white/40 transition-transform duration-300 group-hover:scale-x-150 group-hover:bg-blue-500"></span>
            </a>
        </div>

        <div class="flex w-full flex-col md:w-2/3">
            {#each faqs as item, index}
                <div class="border-b border-white/10 py-6 md:py-8">
                    <button
                        class="group flex w-full cursor-pointer items-center justify-between text-left"
                        onclick={() => toggle(index)}
                        aria-expanded={activeIndex === index}
                    >
                        <span class="pr-6 font-serif text-lg text-white/80 transition-colors duration-300 group-hover:text-white md:text-2xl">
                            {item.q}
                        </span>

                        <div
                            class="flex h-10 w-10 shrink-0 transform items-center justify-center rounded-full bg-white/5 transition-all duration-500 group-hover:bg-white/10"
                            class:rotate-[135deg]={activeIndex === index}
                            class:text-blue-500={activeIndex === index}
                        >
                            <Plus class="h-5 w-5 transition-transform" />
                        </div>
                    </button>

                    {#if activeIndex === index}
                        <div
                            transition:slide={{ duration: 400, easing: (t) => --t * t * t + 1 }}
                            class="overflow-hidden"
                        >
                            <p class="max-w-2xl pt-6 font-sans text-sm font-light leading-relaxed text-white/50 md:text-base">
                                {item.a}
                            </p>
                        </div>
                    {/if}
                </div>
            {/each}
        </div>
    </div>
</section>