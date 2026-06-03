<script>
    import { onMount } from "svelte";
    import gsap from "gsap";
    import ScrollToPlugin from "gsap/ScrollToPlugin";
    import Logo from "./logo.svelte";
    import Menu from "@lucide/svelte/icons/menu";
    import X from "@lucide/svelte/icons/x";
    import Sun from "@lucide/svelte/icons/sun";
    import Moon from "@lucide/svelte/icons/moon";

    let headerRef = $state();
    let navItemsRef = $state([]);
    let iconsRef = $state();
    let logoRef = $state();
    let mobileMenuRef = $state();
    let mobileLinksRef = $state([]);
    let isMenuOpen = $state(false);
    let currentTheme = $state("dark");

    function toggleTheme() {
        const isLight = document.documentElement.classList.toggle("light");
        currentTheme = isLight ? "light" : "dark";
        localStorage.setItem("studio-theme", currentTheme);
    }

    function toggleMenu() {
        isMenuOpen = !isMenuOpen;
        if (isMenuOpen) {
            const tl = gsap.timeline();
            tl.to(mobileMenuRef, {
                autoAlpha: 1,
                clipPath: "inset(0% 0% 0% 0%)",
                duration: 0.6,
                ease: "power3.inOut"
            }).fromTo(
                mobileLinksRef,
                { y: 30, autoAlpha: 0 },
                {
                    y: 0,
                    autoAlpha: 1,
                    duration: 0.5,
                    stagger: 0.08,
                    ease: "power2.out"
                },
                "-=0.2"
            );
        } else {
            gsap.to(mobileMenuRef, {
                autoAlpha: 0,
                clipPath: "inset(0% 100% 0% 0%)",
                duration: 0.5,
                ease: "power3.inOut"
            });
        }
    }

    function scrollTo(evt, id) {
        evt.preventDefault();
        if (isMenuOpen) toggleMenu();
        gsap.to(window, {
            duration: 1.2,
            scrollTo: { y: id, offsetY: 20 },
            ease: "power4.inOut"
        });
    }

    onMount(() => {
        if (typeof window !== "undefined") {
            currentTheme = document.documentElement.classList.contains("light") ? "light" : "dark";
        }

        gsap.registerPlugin(ScrollToPlugin);
        let mm = gsap.matchMedia();

        mm.add(
            {
                isMobile: "(max-width: 767px)",
                isDesktop: "(min-width: 768px)"
            },
            (context) => {
                let { isMobile, isDesktop } = context.conditions;
                const tl = gsap.timeline({ delay: 0.1 });

                gsap.set(headerRef, {
                    width: "0px",
                    opacity: 0
                });
                gsap.set(logoRef, { autoAlpha: 0, y: 10 });
                gsap.set(iconsRef, { autoAlpha: 0, x: 10 });
                gsap.set(mobileMenuRef, { clipPath: "inset(0% 100% 0% 0%)" });

                if (isDesktop) {
                    gsap.set(navItemsRef, { autoAlpha: 0, y: 10 });
                }

                tl.to(headerRef, {
                    width: isMobile ? "calc(100% - 2rem)" : "100%",
                    maxWidth: "896px",
                    opacity: 1,
                    duration: 1,
                    ease: "expo.inOut"
                }).to(
                    logoRef,
                    {
                        autoAlpha: 1,
                        y: 0,
                        duration: 0.8,
                        ease: "power3.out"
                    },
                    "-=0.3"
                );

                if (isDesktop) {
                    tl.to(
                        navItemsRef,
                        {
                            autoAlpha: 1,
                            y: 0,
                            duration: 0.5,
                            stagger: 0.05,
                            ease: "power2.out"
                        },
                        "-=0.4"
                    );
                }

                tl.to(
                    iconsRef,
                    {
                        autoAlpha: 1,
                        x: 0,
                        duration: 0.4,
                        ease: "power2.out"
                    },
                    "-=0.4"
                );

                return () => tl.kill();
            }
        );

        return () => mm.revert();
    });
</script>

<div
    bind:this={headerRef}
    class="fixed top-4 left-1/2 z-50 flex h-[60px] -translate-x-1/2 items-center justify-between border border-white/10 bg-[#0a0a0a]/60 pl-6 pr-2 whitespace-nowrap opacity-0 shadow-2xl backdrop-blur-xl rounded-full"
>
    <a
        href="#hero"
        onclick={(e) => scrollTo(e, "#hero")}
        bind:this={logoRef}
        class="flex-shrink-0 flex items-center justify-center w-auto cursor-pointer mix-blend-difference"
    >
        <Logo />
    </a>

    <div class="absolute left-1/2 -translate-x-1/2 hidden md:block">
        <ul class="flex space-x-8 text-sm font-medium text-white/60">
            <li bind:this={navItemsRef[0]}>
                <a href="#showcase" onclick={(e) => scrollTo(e, "#showcase")} class="hover:text-white transition-colors">Services</a>
            </li>
            <li bind:this={navItemsRef[1]}>
                <a href="#work" onclick={(e) => scrollTo(e, "#work")} class="hover:text-white transition-colors">Selected Work</a>
            </li>
            <li bind:this={navItemsRef[2]}>
                <a href="#stats" onclick={(e) => scrollTo(e, "#stats")} class="hover:text-white transition-colors">Pricing</a>
            </li>
        </ul>
    </div>

    <div bind:this={iconsRef} class="flex items-center space-x-2 z-50">
        <button
            onclick={toggleTheme}
            class="cursor-pointer w-10 h-10 flex justify-center items-center text-white/60 hover:text-white hover:bg-white/10 transition-colors rounded-full"
        >
            {#if currentTheme === "light"}
                <Moon class="w-[18px] h-[18px] text-black" />
            {:else}
                <Sun class="w-[18px] h-[18px] text-white" />
            {/if}
        </button>

        <a
            href="#footer"
            onclick={(e) => scrollTo(e, "#footer")}
            class="hidden md:flex items-center justify-center text-sm font-medium bg-white text-black hover:bg-white/90 transition-colors px-6 py-2 rounded-full"
        >
            Get Started
        </a>
        <button
            onclick={toggleMenu}
            class="cursor-pointer w-10 h-10 flex justify-center items-center text-white/80 hover:text-white hover:bg-white/10 transition-colors md:hidden rounded-full"
        >
            {#if isMenuOpen}
                <X class="w-5 h-5" />
            {:else}
                <Menu class="w-5 h-5" />
            {/if}
        </button>
    </div>
</div>

<div
    bind:this={mobileMenuRef}
    class="fixed inset-0 z-40 bg-[#050505]/95 backdrop-blur-2xl flex flex-col justify-center invisible opacity-0 px-10 overflow-hidden"
>
    <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[300px] h-[300px] bg-blue-600/10 blur-[120px] pointer-events-none rounded-full"></div>

    <ul class="flex flex-col space-y-8 text-left relative z-10">
        <li class="overflow-hidden">
            <a
                bind:this={mobileLinksRef[0]}
                href="#showcase"
                onclick={(e) => scrollTo(e, "#showcase")}
                class="block text-3xl font-sans font-light text-white/70 hover:text-white transition-colors will-change-transform"
            >
                Services
            </a>
        </li>
        <li class="overflow-hidden">
            <a
                bind:this={mobileLinksRef[1]}
                href="#work"
                onclick={(e) => scrollTo(e, "#work")}
                class="block text-3xl font-sans font-light text-white/70 hover:text-white transition-colors will-change-transform"
            >
                Selected Work
            </a>
        </li>
        <li class="overflow-hidden">
            <a
                bind:this={mobileLinksRef[2]}
                href="#stats"
                onclick={(e) => scrollTo(e, "#stats")}
                class="block text-3xl font-sans font-light text-white/70 hover:text-white transition-colors will-change-transform"
            >
                Pricing
            </a>
        </li>
        <li class="overflow-hidden mt-4 pt-6 border-t border-white/10">
            <a
                bind:this={mobileLinksRef[3]}
                href="#footer"
                onclick={(e) => scrollTo(e, "#footer")}
                class="inline-block text-lg font-sans text-white hover:text-white/80 transition-colors will-change-transform"
            >
                Get Started &rarr;
            </a>
        </li>
    </ul>

    <div class="absolute bottom-10 left-10 flex gap-6 text-[10px] font-mono text-white/30 uppercase tracking-widest relative z-10">
        <a href="https://x.com" target="_blank" rel="noreferrer" class="hover:text-white transition-colors">Twitter</a>
        <a href="https://linkedin.com" target="_blank" rel="noreferrer" class="hover:text-white transition-colors">LinkedIn</a>
    </div>
</div>