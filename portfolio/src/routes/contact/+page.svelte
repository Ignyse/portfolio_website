<script>
    const email = "ignacysuspro@gmail.com";

    const socials = [
        {
            name: "LinkedIn",
            url: "https://linkedin.com/in/ignacy-sus"
        },
        {
            name: "GitHub",
            url: "https://github.com/Ignyse"
        }
    ];
</script>

<div class="relative min-h-screen overflow-clip bg-white px-6 py-20">
    <!-- Ambient Background Blobs -->
    <div aria-hidden="true" class="pointer-events-none absolute -left-32 -top-32 h-[28rem] w-[28rem] rounded-full bg-blue-200/50 blur-3xl"></div>
    <div aria-hidden="true" class="pointer-events-none absolute -bottom-20 -right-32 h-[28rem] w-[28rem] rounded-full bg-purple-200/50 blur-3xl"></div>
    <div aria-hidden="true" class="pointer-events-none absolute bottom-10 left-1/2 h-80 w-80 rounded-full bg-pink-200/40 blur-3xl"></div>

    <div class="relative z-10 mx-auto max-w-2xl">
        <header class="mb-16 text-center">
            <p class="mb-1 text-xs font-medium uppercase tracking-widest text-gray-400">
                Get in touch
            </p>
            <h1 class="text-5xl sm:text-6xl font-semibold tracking-tight text-gray-800">
                What arrives by chance becomes opportunity for the one who is open.
            </h1>
        </header>

        <div class="space-y-16">
            <!-- Email Section -->
            <div class="text-center">
                <p class="mb-3 text-sm uppercase tracking-widest text-gray-400">Email</p>
                
                <div class="flex flex-col sm:flex-row items-center justify-center gap-4">
                    <a 
                        href="mailto:{email}"
                        class="text-3xl sm:text-4xl font-medium text-gray-800 hover:text-gray-600 transition-colors"
                    >
                        {email}
                    </a>
<!--  -->
                </div>
            </div>

            <!-- Social Links -->
            <div>
                <p class="mb-6 text-center text-sm uppercase tracking-widest text-gray-400">
                    Elsewhere
                </p>
                
                <div class="flex flex-wrap justify-center gap-4">
                    {#each socials as social}
                        <a
                            href={social.url}
                            target="_blank"
                            rel="noopener noreferrer"
                            class="group px-8 py-4 rounded-2xl bg-white shadow-md shadow-black/5 hover:shadow-xl hover:-translate-y-0.5 transition-all text-lg font-medium text-gray-700 hover:text-gray-900"
                        >
                            {social.name}
                        </a>
                    {/each}
                </div>
            </div>

            <!-- Closing Message -->
            <div class="pt-8 border-t border-gray-100 text-center">
                <p class="max-w-md mx-auto text-gray-500 leading-relaxed">
                    Interested in building from scratch — open to startups, collaborations, full-time roles, 
                    freelance projects, and conversations with ambitious builders.
                </p>
            </div>
        </div>
    </div>
</div>