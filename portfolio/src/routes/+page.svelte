<script>
  const interests = [
    {
      label: 'Composing Music',
      color: '#b49d9d',        // near-black charcoal
      accent: '#4a4a4a',
      x: -22, y: -17,
      delay: '0s',
      description: 'Classically trained in violin, I enjoy creating my own melodies and turning ideas into music.',
    },
    {
      label: 'Water Sports',
      color: '#49677C',        // deep ocean slate
      accent: '#3f5a6e',
      x: 24, y: -15,
      delay: '0.7s',
      description: 'I started swimming at 6, but by 10 I had completed a 1 km lake marathon, and by 12 I had won my first solo sailing competition.',
    },
    {
      label: 'Languages',
      color: '#8a664a',        // warm espresso brown
      accent: '#6b5040',
      x: -26, y: 20,
      delay: '1.4s',
      description: "I learned French at six, and I'm currently challenging myself to learn 한국어.",
    },
    {
      label: 'Coding',
      color: '#2F5C4A',        // dark forest green
      accent: '#2d5443',
      x: 25, y: 22,
      delay: '2.1s',
      description: 'I chose Computer Science to turn logic and creativity into tools that could help people and spark imagination.',
    },
    {
      label: 'Photography',
      color: '#7F1734',        // dark warm sepia
      accent: '#574840',
      x: 0, y: -30,
      delay: '2.8s',
      description: "I'm drawn to nature and animal photography for the detail, calm, and stories found in small moments.",
    },
    {
      label: 'Motivation',
      color: '#53496D',        // deep aubergine
      accent: '#463d58',
      x: 0, y: 30,
      delay: '3.5s',
      description: "The tougher the odds, the more focused I become. I've always been driven to prove limits wrong.",
    }
  ];

  let selected = $state(null);

  function toggle(item) {
    selected = selected?.label === item.label ? null : item;
  }
</script>

<svelte:head>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="anonymous" />
  <link
    href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;1,300;1,400&family=DM+Sans:wght@300;400;500&display=swap"
    rel="stylesheet"
  />
</svelte:head>

<!--
  Linen background, no overflow scroll from blobs
-->
<div class="root">

  <!-- Very subtle grain overlay for matte texture -->
  <div class="grain" aria-hidden="true"></div>

  <!-- Soft ambient wash — barely visible, keeps it warm not sterile -->
  <div class="ambient-top"    aria-hidden="true"></div>
  <div class="ambient-bottom" aria-hidden="true"></div>

  <!-- Click-outside dismissal -->
  {#if selected}
    <button
      type="button"
      aria-label="Dismiss tooltip"
      class="dismiss-overlay"
      onclick={() => (selected = null)}
    ></button>
  {/if}

  <!-- Hero -->
  <div class="hero">
    <h1 class="name">Ignacy Sus</h1>
    <p class="tagline">Builder. Not just a programmer.</p>
    <div class="rule"></div>
  </div>

  <!-- Bubbles -->
  {#each interests as item (item.label)}
    <div
      class="bubble-anchor"
      style="
        left: clamp(12%, calc(50% + {item.x}vw), 88%);
        top:  clamp(11%, calc(50% + {item.y}vh), 89%);
      "
    >
      <div class="float-wrap" style="animation-delay: {item.delay};">

        <!-- Tooltip -->
        {#if selected?.label === item.label}
          <div
            role="tooltip"
            id="tip-{item.label.replace(/\s+/g, '-')}"
            class="tooltip"
          >
            {item.description}
            <span aria-hidden="true" class="caret"></span>
          </div>
        {/if}

        <!-- The pill -->
        <button
          type="button"
          aria-pressed={selected?.label === item.label}
          aria-describedby={selected?.label === item.label
            ? `tip-${item.label.replace(/\s+/g, '-')}`
            : undefined}
          onclick={(e) => { e.stopPropagation(); toggle(item); }}
          class="pill"
          class:pill--active={selected?.label === item.label}
          style="
            --pill-bg: {item.color};
            --pill-hover: {item.accent};
          "
        >
          {item.label}
        </button>

      </div>
    </div>
  {/each}
</div>

<style>
  /* ── Tokens ───────────────────────────────────────────── */
  :global(body) {
    margin: 0;
    padding: 0;
    background: #F5F0E8;
  }

  /* ── Root ─────────────────────────────────────────────── */
  .root {
    font-family: 'DM Sans', sans-serif;
    position: relative;
    height: 100svh;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    background: #F5F0E8;
  }

  /* ── Grain texture ────────────────────────────────────── */
  .grain {
    position: absolute;
    inset: 0;
    pointer-events: none;
    z-index: 1;
    opacity: 0.045;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
    background-size: 180px 180px;
  }

  /* ── Ambient washes ───────────────────────────────────── */
  .ambient-top {
    position: absolute;
    top: -10%;
    left: 50%;
    transform: translateX(-50%);
    width: 70vw;
    height: 50vh;
    border-radius: 50%;
    background: radial-gradient(ellipse, rgba(180,160,130,0.18) 0%, transparent 70%);
    pointer-events: none;
    z-index: 0;
  }
  .ambient-bottom {
    position: absolute;
    bottom: -10%;
    left: 50%;
    transform: translateX(-50%);
    width: 50vw;
    height: 40vh;
    border-radius: 50%;
    background: radial-gradient(ellipse, rgba(120,100,80,0.10) 0%, transparent 70%);
    pointer-events: none;
    z-index: 0;
  }

  /* ── Dismiss overlay ──────────────────────────────────── */
  .dismiss-overlay {
    position: absolute;
    inset: 0;
    z-index: 10;
    cursor: default;
    background: transparent;
    border: none;
  }

  /* ── Hero ─────────────────────────────────────────────── */
  .hero {
    position: relative;
    z-index: 20;
    text-align: center;
    pointer-events: none;
    user-select: none;
  }

  .name {
    font-family: 'Cormorant Garamond', Georgia, serif;
    font-weight: 300;
    font-size: clamp(2.8rem, 7vw, 5.5rem);
    letter-spacing: -0.01em;
    color: #1A1714;
    margin: 0 0 0.25rem;
    line-height: 1;
  }

  .tagline {
    font-family: 'DM Sans', sans-serif;
    font-weight: 300;
    font-size: clamp(0.75rem, 1.4vw, 1rem);
    letter-spacing: 0.18em;
    text-transform: uppercase;
    color: #9A8F83;
    margin: 0 0 1.4rem;
  }

  /* Thin decorative rule below tagline */
  .rule {
    width: 2.5rem;
    height: 1px;
    background: #C8BFB4;
    margin: 0 auto;
  }

  /* ── Bubble anchor ────────────────────────────────────── */
  .bubble-anchor {
    position: absolute;
    z-index: 20;
    transform: translate(-50%, -50%);
  }

  /* ── Float animation wrapper ──────────────────────────── */
  .float-wrap {
    animation: float 5s ease-in-out infinite;
  }

  /* ── Tooltip ──────────────────────────────────────────── */
  .tooltip {
    position: absolute;
    bottom: calc(100% + 10px);
    left: 50%;
    transform: translateX(-50%);
    background: #FDFAF6;
    border: 1px solid #DDD6CC;
    border-radius: 10px;
    padding: 0.65rem 0.9rem;
    width: max-content;
    max-width: 200px;
    text-align: center;
    font-size: 0.75rem;
    line-height: 1.55;
    color: #4A443D;
    font-weight: 300;
    letter-spacing: 0.01em;
    box-shadow: 0 4px 20px rgba(30,20,10,0.09), 0 1px 4px rgba(30,20,10,0.06);
    pointer-events: none;
    animation: fade-in 0.18s ease-out;
  }

  .caret {
    position: absolute;
    top: 100%;
    left: 50%;
    transform: translateX(-50%);
    border: 5px solid transparent;
    border-top-color: #DDD6CC;
  }
  /* inner caret covers border line */
  .caret::after {
    content: '';
    position: absolute;
    top: -6px;
    left: -4px;
    border: 4px solid transparent;
    border-top-color: #FDFAF6;
  }

  /* ── Pill ─────────────────────────────────────────────── */
  .pill {
    display: flex;
    align-items: center;
    justify-content: center;
    border: none;
    outline: none;
    cursor: pointer;
    border-radius: 999px;
    font-family: 'DM Sans', sans-serif;
    font-weight: 400;
    letter-spacing: 0.04em;
    font-size: clamp(0.8rem, 1.1vw, 2rem);
    color: #F0EBE3;
    background: var(--pill-bg);
    /* Matte depth: top-light bevel + bottom shadow */
    box-shadow:
      inset 0 1px 0 rgba(255,255,255,0.10),
      inset 0 -1px 0 rgba(0,0,0,0.15),
      0 2px 8px rgba(0,0,0,0.18),
      0 1px 2px rgba(0,0,0,0.12);
    /* padding is basically the width here*/
    padding: clamp(1.4rem, 2.5vw, 2rem);
    height: clamp(2rem, 1vh, 3rem);
    white-space: nowrap;
    max-width: clamp(150px, 22vw, 220px);
    transition:
      transform 0.25s cubic-bezier(0.34,1.56,0.64,1),
      box-shadow 0.25s ease,
      background 0.2s ease;
  }

  .pill:hover,
  .pill--active {
    background: var(--pill-hover);
    transform: scale(1.07) translateY(-1px);
    box-shadow:
      inset 0 1px 0 rgba(255,255,255,0.13),
      inset 0 -1px 0 rgba(0,0,0,0.2),
      0 6px 18px rgba(0,0,0,0.22),
      0 2px 4px rgba(0,0,0,0.14);
  }

  .pill:active {
    transform: scale(0.96);
    transition-duration: 0.1s;
  }

  .pill:focus-visible {
    outline: 2px solid #9A8F83;
    outline-offset: 3px;
  }

  /* ── Animations ───────────────────────────────────────── */
  @keyframes float {
    0%, 100% { transform: translateY(0);     }
    50%       { transform: translateY(-8px);  }
  }

  @keyframes fade-in {
    from { opacity: 0; transform: translateX(-50%) translateY(4px); }
    to   { opacity: 1; transform: translateX(-50%) translateY(0);   }
  }
</style>