<script>
    import Logo from "./logo.svelte";
</script>

<footer
    id="contact"
    class="relative w-full overflow-hidden border-t border-b-8 border-b-white/5 border-white/10 bg-[#050505] pt-32 pb-12 text-white select-none"
>
    <div class="mx-auto mb-32 flex max-w-7xl flex-col items-center justify-between gap-12 px-6 md:flex-row md:px-24">
        <div class="w-full md:w-2/3">
            <div class="mb-4 flex items-center gap-2">
                <span class="relative flex h-2 w-2">
                    <span class="absolute inline-flex h-full w-full animate-ping rounded-full bg-emerald-400 opacity-75"></span>
                    <span class="relative inline-flex h-2 w-2 rounded-full bg-emerald-500"></span>
                </span>
                <span class="font-mono text-[10px] uppercase tracking-widest text-emerald-400/80">Available for Q3 2026</span>
            </div>
            <h2 class="z-10 font-serif text-[12vw] leading-[0.85] tracking-tighter mix-blend-difference md:text-[7vw]">
                Have a project<br />
                <span class="italic text-white/40">in mind?</span>
            </h2>
        </div>
        <div class="z-10 flex w-full md:w-1/3 md:justify-end">
            <a
                href="https://cal.com/tanviramin/discovery"
                data-cal-link="tanviramin/discovery"
                class="group relative flex h-40 w-40 cursor-pointer items-center justify-center rounded-full bg-white text-black transition-transform duration-500 transform-gpu hover:scale-105 md:h-48 md:w-48"
            >
                <span class="absolute inset-0 z-0 origin-center scale-0 rounded-full bg-blue-600 transition-transform duration-500 ease-out group-hover:scale-100"></span>
                <span class="relative z-10 font-sans text-base font-medium tracking-wide transition-colors duration-500 group-hover:text-white md:text-lg">
                    Let's Talk
                </span>
            </a>
        </div>
    </div>

    <div class="relative z-10 mx-auto mb-24 grid max-w-7xl grid-cols-1 gap-12 px-6 md:grid-cols-4 md:gap-4 md:px-24">
        <div class="col-span-1 flex flex-col gap-6">
            <div class="opacity-90">
                <Logo />
            </div>
            <p class="max-w-xs font-sans text-sm leading-relaxed text-white/40">
                Architecting high-performance digital ecosystems with extreme technical engineering precision.
            </p>
        </div>

        <div class="col-span-1 flex flex-col gap-4">
            <h4 class="mb-2 font-mono text-[10px] uppercase tracking-[0.2em] text-blue-500">
                Navigation
            </h4>
            <a href="#manifesto" class="w-fit font-sans text-sm text-white/60 transition-colors hover:text-white">Manifesto</a>
            <a href="#services" class="w-fit font-sans text-sm text-white/60 transition-colors hover:text-white">Capabilities</a>
            <a href="#work" class="w-fit font-sans text-sm text-white/60 transition-colors hover:text-white">Selected Works</a>
            <a href="#faq" class="w-fit font-sans text-sm text-white/60 transition-colors hover:text-white">FAQ</a>
        </div>

        <div class="col-span-1 flex flex-col gap-4">
            <h4 class="mb-2 font-mono text-[10px] uppercase tracking-[0.2em] text-blue-500">
                Networks
            </h4>
            <a href="https://tanviramin.is-a.dev" target="_blank" rel="noopener noreferrer" class="w-fit font-sans text-sm text-white/60 transition-colors hover:text-white">Portfolio</a>
            <a href="https://github.com/tanviramin-dev" target="_blank" rel="noopener noreferrer" class="w-fit font-sans text-sm text-white/60 transition-colors hover:text-white">GitHub</a>
            <a href="https://linkedin.com" target="_blank" rel="noopener noreferrer" class="w-fit font-sans text-sm text-white/60 transition-colors hover:text-white">LinkedIn</a>
        </div>

        <div class="col-span-1 flex flex-col gap-4">
            <h4 class="mb-2 font-mono text-[10px] uppercase tracking-[0.2em] text-blue-500">
                Operations
            </h4>
            <p class="font-sans text-sm leading-relaxed text-white/40 mb-2">
                Building clean, production-ready full-stack applications with optimal rendering states.
            </p>
            <a href="mailto:tanviramin.dev@gmail.com" class="font-mono text-xs text-white/60 hover:text-blue-500 transition-colors">tanviramin.dev@gmail.com</a>
        </div>
    </div>

    <div class="relative z-10 mx-auto pt-8 border-t border-white/10 flex flex-col md:flex-row justify-between items-center gap-6 px-6 text-[11px] font-mono tracking-wider text-white/30 md:px-24">
        <div class="flex flex-col gap-2 md:flex-row md:gap-6">
            <p>&copy; 2026 Tanvir Amin. All Rights Reserved.</p>
            <div class="flex gap-4">
                <span class="hover:text-white/60 transition-colors cursor-pointer">Terms of Service</span>
                <span class="hover:text-white/60 transition-colors cursor-pointer">Privacy Policy</span>
            </div>
        </div>

        <div class="flex flex-col items-center gap-4 md:flex-row md:gap-8">
            <span class="font-sans text-xs font-light text-white/40">
                Engineered by 
                <a
                    href="https://tanviramin.is-a.dev"
                    target="_blank"
                    rel="noopener noreferrer"
                    class="font-medium text-blue-500 transition-colors duration-300 hover:text-white hover:underline underline-offset-4"
                >
                    Tanvir Amin
                </a>
            </span>
        </div>
    </div>

    <div class="pointer-events-none absolute bottom-0 left-1/2 h-[400px] w-screen -translate-x-1/2 rounded-full bg-blue-600/[0.03] blur-[200px]"></div>
</footer>