<script>
    import { onMount } from "svelte";
    import gsap from "gsap";
    import ScrollTrigger from "gsap/ScrollTrigger";

    let statsRef = $state();

    const stats = [
        { label: "Success Rate", limit: 100, suffix: "%", prefix: "" },
        { label: "Production Apps", limit: 12, suffix: "+", prefix: "" },
        { label: "Delivery Cycle", limit: 14, suffix: " Days", prefix: "<" },
        { label: "Uptime SLA", limit: 99, suffix: ".9%", prefix: "" }
    ];

    const tiers = [
        {
            name: "Fixed Scope",
            price: "$3,500",
            period: "per project",
            desc: "Best for production-ready landing pages, MVP systems, and high-conversion interactive digital assets.",
            features: [
                "14-Day Delivery Cycle",
                "Direct Architect Communication",
                "Production-Ready Svelte/Next.js Codebase",
                "Serverless Deployment Setup",
                "Complete System Documentation"
            ],
            cta: "Book Discovery Call",
            link: "https://cal.com/tanviramin/discovery"
        },
        {
            name: "Monthly Retainer",
            price: "$5,000",
            period: "per month",
            desc: "Best for scaling systems, deep full-stack feature development, and long-term architectural infrastructure.",
            features: [
                "Dedicated Development Capacity",
                "Asynchronous Linear / Trello Backlog",
                "Enterprise Architecture & Security",
                "Optimal Rendering Optimizations",
                "Pause or Cancel Anytime"
            ],
            cta: "Secure Retainer Slots",
            link: "https://cal.com/tanviramin/retainer"
        }
    ];

    onMount(() => {
        gsap.registerPlugin(ScrollTrigger);

        const counts = statsRef.querySelectorAll(".counterData");
        const tweens = [];

        counts.forEach((counter, i) => {
            let target = stats[i].limit;
            let obj = { val: 0 };

            const t = gsap.to(obj, {
                val: target,
                duration: 2,
                ease: "power3.out",
                scrollTrigger: {
                    trigger: statsRef,
                    start: "top 85%"
                },
                onUpdate: () => {
                    counter.innerText = Math.floor(obj.val);
                }
            });
            tweens.push(t);
        });

        return () => {
            tweens.forEach((t) => {
                t.scrollTrigger?.kill();
                t.kill();
            });
        };
    });
</script>

<section
    bind:this={statsRef}
    class="relative z-10 w-full border-b border-t border-white/5 bg-[#050505] py-24 text-white md:py-32 select-none"
>
    <div class="mx-auto grid max-w-7xl grid-cols-2 gap-12 px-6 text-left md:grid-cols-4 md:gap-8 md:px-24 md:text-center">
        {#each stats as stat}
            <div class="flex flex-col gap-2 md:items-center">
                <h4 class="mb-2 flex items-baseline font-serif text-4xl tracking-tight text-white md:justify-center md:text-6xl">
                    {#if stat.prefix}
                        <span class="mr-1 font-sans text-2xl text-white/30 md:text-4xl">{stat.prefix}</span>
                    {/if}
                    <span class="counterData text-blue-500">0</span>
                    <span class="font-sans text-xl text-white/60 md:text-3xl">{stat.suffix}</span>
                </h4>
                <p class="font-mono text-[10px] uppercase tracking-[0.2em] text-white/40">
                    {stat.label}
                </p>
            </div>
        {/each}
    </div>

    <div class="mx-auto mt-32 max-w-5xl px-6 md:px-12">
        <div class="mb-16 text-center">
            <span class="font-mono text-[10px] uppercase tracking-[0.3em] text-blue-500">
                Investment Structure
            </span>
            <h3 class="mt-3 font-serif text-3xl tracking-tight text-white/90 md:text-4xl">
                Productized Engagement Models
            </h3>
        </div>

        <div class="grid grid-cols-1 gap-8 md:grid-cols-2">
            {#each tiers as tier}
                <div class="flex flex-col justify-between border border-white/5 bg-[#0a0a0a] p-8 md:p-12 rounded-none relative overflow-hidden group hover:border-white/10 transition-colors duration-300">
                    <div>
                        <h4 class="font-mono text-xs uppercase tracking-widest text-white/40 mb-4">
                            {tier.name}
                        </h4>
                        <div class="flex items-baseline gap-2 mb-6">
                            <span class="font-serif text-4xl md:text-5xl text-white font-medium">{tier.price}</span>
                            <span class="font-sans text-xs text-white/40 font-light">{tier.period}</span>
                        </div>
                        <p class="font-sans text-sm leading-relaxed text-white/50 mb-8 font-light">
                            {tier.desc}
                        </p>
                        
                        <div class="h-px w-full bg-white/5 mb-8"></div>
                        
                        <ul class="flex flex-col gap-4 mb-12">
                            {#each tier.features as feature}
                                <li class="flex items-center gap-3 font-sans text-sm text-white/60 font-light">
                                    <span class="w-1.5 h-1.5 bg-blue-500 rounded-none shrink-0"></span>
                                    <span>{feature}</span>
                                </li>
                            {/each}
                        </ul>
                    </div>

                    <a
                        href={tier.link}
                        data-cal-link={tier.link.replace("https://cal.com/", "")}
                        class="w-full py-4 bg-white text-black font-mono text-xs uppercase tracking-widest text-center transition-transform transform-gpu hover:scale-[1.02] active:scale-[0.98]"
                    >
                        {tier.cta}
                    </a>
                </div>
            {/each}
        </div>
    </div>
</section>