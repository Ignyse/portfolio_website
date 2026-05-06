<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';
	let { children } = $props();
</script>

<header class="fixed top-0 left-0 w-full z-50 backdrop-blur-md bg-white/70 border-b border-black/5">
  <div class="max-w-5xl mx-auto px-6 py-4 flex items-center justify-between">

    <!-- Brand -->
    <a href="/" class="text-sm font-semibold tracking-wide text-black/80 hover:text-black transition">
      Ignacy Sus
    </a>

    <!-- Nav -->
    <nav class="flex items-center gap-8 text-sm">
      <a href="/" class="relative text-black/70 hover:text-black transition group">
        Home
        <span class="absolute left-0 -bottom-1 h-[1px] w-full bg-black scale-x-0 group-hover:scale-x-100 transition-transform origin-left"></span>
      </a>

      <a href="/projects" class="relative text-black/70 hover:text-black transition group">
        Projects
        <span class="absolute left-0 -bottom-1 h-[1px] w-full bg-black scale-x-0 group-hover:scale-x-100 transition-transform origin-left"></span>
      </a>

      <a href="/contact" class="relative text-black/70 hover:text-black transition group">
        Contact
        <span class="absolute left-0 -bottom-1 h-[1px] w-full bg-black scale-x-0 group-hover:scale-x-100 transition-transform origin-left"></span>
      </a>
    </nav>

  </div>
</header>
<main class="pt-20">
{@render children()}
</main>

