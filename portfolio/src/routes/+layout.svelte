<!-- <script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';
	let { children } = $props();
</script>

<header class="fixed top-0 left-0 w-full z-50 backdrop-blur-md bg-white/70 border-b border-black/5">
  <div class="max-w-5xl mx-auto px-6 py-4 flex items-center justify-between">


    <a href="/" class="text-sm font-semibold tracking-wide text-black/80 hover:text-black transition">
      Ignacy Sus
    </a>


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
<main class="pt-10">
{@render children()}
</main>
 -->

 <script lang="ts">
  import './layout.css';
  import favicon from '$lib/assets/favicon.svg';
  import { page } from '$app/stores';

  let { children } = $props();
</script>

<svelte:head>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="anonymous" />
  <link
    href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;1,300&family=DM+Sans:wght@300;400;500&display=swap"
    rel="stylesheet"
  />
  <link rel="icon" href={favicon} />
</svelte:head>

<header class="site-header">
  <div class="header-inner">

    <!-- Brand -->
    <a href="/" class="brand">
      <span class="brand-name">Ignacy Sus</span>
      <span class="brand-dot" aria-hidden="true"></span>
    </a>

    <!-- Nav -->
    <nav class="nav" aria-label="Main navigation">
      {#each [['/', 'Home'], ['/projects', 'Projects'], ['/contact', 'Contact']] as [href, label]}
        <a
          {href}
          class="nav-link"
          class:nav-link--active={$page.url.pathname === href}
          aria-current={$page.url.pathname === href ? 'page' : undefined}
        >
          {label}
        </a>
      {/each}
    </nav>

  </div>
</header>

<main class="site-main">
  {@render children()}
</main>

<style>
  /* ── Design tokens (shared across whole site) ─────────── */
  :global(:root) {
    --linen:        #F5F0E8;
    --linen-card:   #FDFAF6;
    --ink:          #1A1714;
    --ink-mid:      #4A443D;
    --ink-muted:    #9A8F83;
    --border:       #DDD6CC;
    --border-light: #EAE4DA;
    --shadow-warm:  rgba(30, 20, 10, 0.08);

    --font-display: 'Cormorant Garamond', Georgia, serif;
    --font-body:    'DM Sans', system-ui, sans-serif;
  }

  :global(*, *::before, *::after) { box-sizing: border-box; }

  :global(body) {
    margin: 0;
    padding: 0;
    background: var(--linen);
    font-family: var(--font-body);
    -webkit-font-smoothing: antialiased;
    color: var(--ink);
  }

  /* ── Header ───────────────────────────────────────────── */
  .site-header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    z-index: 50;
    /* Very light linen tint — blends with page, not harsh white */
    background: rgba(245, 240, 232, 0.82);
    backdrop-filter: blur(14px);
    -webkit-backdrop-filter: blur(14px);
    border-bottom: 1px solid var(--border-light);
  }

  .header-inner {
    max-width: 64rem;
    margin: 0 auto;
    padding: 0 1.5rem;
    height: 3.25rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  /* Brand */
  .brand {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    text-decoration: none;
  }

  .brand-name {
    font-family: var(--font-display);
    font-weight: 400;
    font-size: 1.05rem;
    letter-spacing: 0.02em;
    color: var(--ink);
    transition: color 0.2s;
  }
  .brand:hover .brand-name { color: var(--ink-mid); }

  /* Tiny decorative separator dot */
  .brand-dot {
    display: block;
    width: 3px;
    height: 3px;
    border-radius: 50%;
    background: var(--ink-muted);
  }

  /* Nav */
  .nav {
    display: flex;
    align-items: center;
    gap: 2rem;
  }

  .nav-link {
    position: relative;
    font-family: var(--font-body);
    font-weight: 300;
    font-size: 0.8rem;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    text-decoration: none;
    color: var(--ink-muted);
    transition: color 0.2s;
    padding-bottom: 2px;
  }

  /* Underline rule — slides in from left on hover/active */
  .nav-link::after {
    content: '';
    position: absolute;
    bottom: -1px;
    left: 0;
    width: 100%;
    height: 1px;
    background: var(--ink);
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.25s cubic-bezier(0.4, 0, 0.2, 1);
  }

  .nav-link:hover,
  .nav-link--active {
    color: var(--ink);
  }

  .nav-link:hover::after,
  .nav-link--active::after {
    transform: scaleX(1);
  }

  /* ── Main ─────────────────────────────────────────────── */
  .site-main {
    padding-top: 3.25rem; /* exactly header height — no gap, no overlap */
  }
</style>
