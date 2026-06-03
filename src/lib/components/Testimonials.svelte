<script>
    import { onMount } from "svelte";
    import gsap from "gsap";

    const feedbacks = [
        {
            name: "Sarah Jenkins",
            role: "Product Owner",
            text: "Working directly with a single engineer who understands both pixel-perfect frontend and complex backend architecture cut our development overhead completely in half."
        },
        {
            name: "Marcus Thorne",
            role: "Tech Founder",
            text: "Zero communication friction and sheer execution power. The clean code architecture and performance metrics delivered on production exceeded our standards."
        },
        {
            name: "Elena Rostova",
            role: "Operations Director",
            text: "He redefined our core application flow. Having a one-man army handle everything from technical layout design to secure server deployment was absolute gold."
        }
    ];

    let currentIndex = $state(0);
    let quoteRef = $state();
    let nameRef = $state();
    let isAnimating = false;
    let timer;

    function resetTimer() {
        if (timer) clearInterval(timer);
        timer = setInterval(nextQuote, 6000);
    }

    function nextQuote() {
        if (isAnimating) return;
        goToQuote((currentIndex + 1) % feedbacks.length);
    }

    function goToQuote(index) {
        if (index === currentIndex || isAnimating) return;
        isAnimating = true;

        if (timer) clearInterval(timer);

        gsap.to([quoteRef, nameRef], {
            autoAlpha: 0,
            y: 15,
            duration: 0.4,
            ease: "power2.inOut",
            onComplete: () => {
                currentIndex = index;
                
                gsap.fromTo(
                    [quoteRef, nameRef],
                    { autoAlpha: 0, y: -15 },
                    {
                        autoAlpha: 1,
                        y: 0,
                        duration: 0.6,
                        stagger: 0.1,
                        ease: "power2.out",
                        onComplete: () => {
                            isAnimating = false;
                            resetTimer();
                        }
                    }
                );
            }
        });
    }

    onMount(() => {
        resetTimer();
        return () => {
            if (timer) clearInterval(timer);
        };
    });
</script>

<section
    id="testimonials"
    class="relative z-10 flex w-full overflow-hidden border-t border-white/5 bg-[#050505] py-32 text-white md:py-48 select-none"
>
    <div class="pointer-events-none absolute top-1/2 left-1/2 h-[500px] w-full max-w-[800px] -translate-x-1/2 -translate-y-1/2 rounded-full bg-blue-500/[0.03] blur-[200px]"></div>

    <div class="relative z-10 mx-auto flex w-full max-w-5xl flex-col items-center px-6 text-center md:px-12">
        <span class="mb-16 font-mono text-[10px] uppercase tracking-[0.3em] text-white/30">
            Client Voices
        </span>

        <div class="flex min-h-[180px] items-center justify-center md:min-h-[150px]">
            <h3
                bind:this={quoteRef}
                class="max-w-4xl font-serif text-xl leading-relaxed tracking-tight text-white/90 md:text-3xl lg:text-4xl will-change-transform"
            >
                "{feedbacks[currentIndex].text}"
            </h3>
        </div>

        <div bind:this={nameRef} class="mt-12 flex flex-col items-center gap-2 will-change-transform">
            <h4 class="font-sans text-xs font-semibold uppercase tracking-[0.2em] text-white">
                {feedbacks[currentIndex].name}
            </h4>
            <span class="font-sans text-sm text-white/40">
                {feedbacks[currentIndex].role}
            </span>
        </div>

        <div class="mt-16 flex gap-3">
            {#each feedbacks as _, i}
                <button
                    class="h-1.5 rounded-full transition-all duration-300 cursor-pointer {currentIndex === i ? 'w-8 bg-blue-500' : 'w-2 bg-white/20 hover:bg-white/40'}"
                    aria-label="Go to slide {i + 1}"
                    onclick={() => goToQuote(i)}
                ></button>
            {/each}
        </div>
    </div>
</section>