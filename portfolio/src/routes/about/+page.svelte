<script>
  import { onMount } from 'svelte';

  // ── Timeline data ──────────────────────────────────────────────────────────
  const milestones = [
    {
      id: 'ib',
      year: '2021',
      place: 'Warsaw, Poland',
      icon: '✦',
      title: 'International Baccalaureate',
      badge: '44 / 45',
      badgeLabel: 'IB Score',
      body: 'Finished in the global top percentile with a near-perfect score — one of the strongest results in the World.',
      decision: {
        prompt: 'University offers received',
        options: [
          { label: 'University of Warsaw',  chosen: false },
          { label: 'University of Warwick', chosen: false, note: 'scholarship' },
          { label: 'University of Edinburgh', chosen: false },
          { label: 'TU Delft',              chosen: false },
          { label: 'Trinity College Dublin', chosen: true  },
        ],
      },
    },
    {
      id: 'tcd',
      year: '2021-2023',
      place: 'Dublin, Ireland',
      icon: '◈',
      title: 'Trinity College Dublin',
      badge: 'Years 1 – 2',
      badgeLabel: 'Computer Science',
      body: 'Built a strong foundation in algorithms, systems, mathematical and statistical thinking, and software engineering at one of Europe’s oldest universities.',
      decision: null, // no fork here — just progression
    },
    {
      id: 'exchange',
      year: '2023-2024',
      place: 'Lyon, France',
      icon: '◉',
      title: 'Third-Year Exchange',
      badge: 'Year 3',
      badgeLabel: 'Year Abroad',
      body: 'Qualified for an international exchange — two very different paths, two very different bets. Studied in another language and had to adapt quickly to a new academic system, but adapted smoothly and integrated well.',
      decision: {
        prompt: 'Exchange destination',
        options: [
          { label: 'University of Toronto', chosen: false },
          { label: 'INSA Lyon',             chosen: true  },
        ],
      },
    },
    {
      id: 'ecb',
      year: '2025',
      place: 'Frankfurt, Germany',
      icon: '◈',
      title: 'European Central Bank',
      badge: 'Intern',
      badgeLabel: 'Sofware, Information and Systems Engineering',
      body: 'Chose institutional depth over comfort — engineering at the bank that sets monetary policy for 350 million people.',
      decision: {
        prompt: 'After third year',
        options: [
          { label: 'SWE — Dublin',    chosen: false },
          { label: 'SWE — Elsewhere', chosen: false },
          { label: 'ECB Frankfurt',   chosen: true  },
        ],
      },
    },
    {
      id: 'tcd5',
      year: '2025-2026',
      place: 'Dublin, Ireland',
      icon: '◈',
      title: 'Trinity College Dublin',
      badge: 'Master Year',
      badgeLabel: 'Computer Science - Graduated with Distinction',
      body: 'Wrote an interdisciplinary Master’s thesis across computer science, neuroscience, psychology, linguistics, and cognitive science, applying machine learning to neural activity data. The work required integrating knowledge across multiple domains and had a high entry barrier. Furthermore, I strengthened my understanding of advanced topics such as quantum networks and cybersecurity & privacy.',
      decision: {
        prompt: 'Possible Master Thesis Topics',
        options: [
          { label: 'Mundane and typical CS topic', chosen: false },
          { label: 'Novel and interdisciplinary with real-world applications',   chosen: true  },
        ],
      },
    },
    {
      id: 'now',
      year: '2026+',
      place: 'The Open Question',
      icon: '?',
      title: 'Every path is still open.',
      badge: '?',
      badgeLabel: 'What\'s next',
      body: '',
      decision: null,
      isQuestion: true,
    },
  ];

  // ── Scroll reveal ──────────────────────────────────────────────────────────
  let visible = $state({});
  let nodes = [];

  onMount(() => {
    const io = new IntersectionObserver(
      (entries) => {
        entries.forEach((e) => {
          if (e.isIntersecting) {
            visible[e.target.dataset.id] = true;
          }
        });
      },
      { threshold: 0.18 }
    );
    nodes.forEach((n) => n && io.observe(n));
    return () => io.disconnect();
  });
</script>

<div class="page">
  <div class="grain" aria-hidden="true"></div>
  <div class="ambient ambient--tl" aria-hidden="true"></div>
  <div class="ambient ambient--br" aria-hidden="true"></div>

  <div class="inner">

    <!-- Page header -->
    <header class="page-header">
      <p class="eyebrow">The journey so far</p>
      <h1 class="page-title">About</h1>
      <div class="rule"></div>
      <p class="page-sub">
        Every choice below closed some doors and opened others.  <br>
        <em>It is only by risking ... that we live at all. (William James)</em>
      </p>
    </header>

    <!-- Timeline -->
    <div class="timeline" role="list">

      {#each milestones as m, i (m.id)}
        <!-- Connecting line segment (drawn between nodes) -->
        {#if i > 0}
          <div
            class="line-segment"
            class:line-segment--visible={visible[milestones[i - 1].id]}
          ></div>
        {/if}

        <!-- Node -->
        <div
          class="node"
          class:node--visible={visible[m.id]}
          class:node--question={m.isQuestion}
          data-id={m.id}
          role="listitem"
          bind:this={nodes[i]}
        >
          <!-- Left: year + place -->
          <div class="node-meta">
            <span class="node-year">{m.year}</span>
            <span class="node-place">{m.place}</span>
          </div>

          <!-- Centre: icon dot -->
          <div class="node-dot" class:node-dot--question={m.isQuestion}>
            <span class="node-icon" aria-hidden="true">{m.icon}</span>
          </div>

          <!-- Right: card -->
          <div class="node-card" class:node-card--question={m.isQuestion}>

            <!-- Badge -->
            <div class="card-badge-row">
              <span class="badge">{m.badge}</span>
              <span class="badge-label">{m.badgeLabel}</span>
            </div>

            <!-- Title -->
            <h2 class="card-title" class:card-title--question={m.isQuestion}>
              {m.title}
            </h2>

            <!-- Body -->
            <p class="card-body">{m.body}</p>

            <!-- Decision fork -->
            {#if m.decision}
              <div class="decision">
                <p class="decision-prompt">{m.decision.prompt}</p>
                <div class="options">
                  {#each m.decision.options as opt}
                    <span
                      class="option"
                      class:option--chosen={opt.chosen}
                      class:option--rejected={!opt.chosen}
                    >
                      {opt.label}
                      {#if opt.note}
                        <em class="option-note">{opt.note}</em>
                      {/if}
                      {#if opt.chosen}
                        <span class="chosen-mark" aria-label="chosen">✓</span>
                      {/if}
                    </span>
                  {/each}
                </div>
              </div>
            {/if}

            <!-- Question mark pulse for final node -->
            {#if m.isQuestion}
              <div class="question-pulse" aria-hidden="true">
                <span>?</span>
              </div>
            {/if}

          </div>
        </div>
      {/each}

    </div>

  </div>
</div>

<style>
  /* ── Page shell ─────────────────────────────────────── */
  .page {
    position: relative;
    min-height: 100svh;
    overflow: hidden;
    background: var(--linen);
    padding: 5rem 1.5rem 7rem;
  }

  .grain {
    position: absolute; inset: 0;
    pointer-events: none; z-index: 1; opacity: 0.045;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
    background-size: 180px 180px;
  }

  .ambient { position: absolute; pointer-events: none; z-index: 0; border-radius: 50%; }
  .ambient--tl {
    top: -6rem; left: -6rem; width: 30rem; height: 30rem;
    background: radial-gradient(ellipse, rgba(180,160,130,0.14) 0%, transparent 70%);
  }
  .ambient--br {
    bottom: -6rem; right: -4rem; width: 24rem; height: 24rem;
    background: radial-gradient(ellipse, rgba(120,100,80,0.09) 0%, transparent 70%);
  }

  /* ── Inner ──────────────────────────────────────────── */
  .inner {
    position: relative; z-index: 10;
    max-width: 52rem; margin: 0 auto;
  }

  /* ── Page header ────────────────────────────────────── */
  .page-header { margin-bottom: 4rem; }

  .eyebrow {
    font-family: var(--font-body);
    font-weight: 300; font-size: 0.7rem;
    letter-spacing: 0.2em; text-transform: uppercase;
    color: var(--ink-muted); margin: 0 0 0.5rem;
  }

  .page-title {
    font-family: var(--font-display);
    font-weight: 300; font-size: clamp(2.4rem, 5vw, 4rem);
    letter-spacing: -0.01em; color: var(--ink);
    margin: 0 0 1rem; line-height: 1;
  }

  .rule { width: 2.5rem; height: 1px; background: var(--border); margin: 0 0 1rem; }

  .page-sub {
    font-family: var(--font-body);
    font-weight: 300; font-size: 0.88rem;
    line-height: 1.7; color: var(--ink-muted); margin: 0;
    max-width: 28rem;
  }
  .page-sub em { font-style: italic; color: var(--ink-mid); }

  /* ── Timeline container ─────────────────────────────── */
  .timeline {
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }

  /* ── Connector line between nodes ───────────────────── */
  .line-segment {
    /* sits in the centre column, 2px wide, grows from 0 height */
    align-self: center;
    /* offset to align with the dot column */
    margin-left: clamp(5rem, 18vw, 8rem);
    width: 1px;
    height: 0;
    background: linear-gradient(to bottom, var(--border), var(--border-light));
    transition: height 0.7s cubic-bezier(0.4,0,0.2,1);
  }

  .line-segment--visible { height: 3rem; }

  /* ── Node row ───────────────────────────────────────── */
  .node {
    display: grid;
    grid-template-columns: clamp(4.5rem, 15vw, 7rem)  /* meta */
                           2.25rem                      /* dot  */
                           1fr;                         /* card */
    align-items: start;
    gap: 0 1.25rem;
    /* Entrance */
    opacity: 0;
    transform: translateY(24px);
    transition: opacity 0.65s cubic-bezier(0.22,1,0.36,1),
                transform 0.65s cubic-bezier(0.22,1,0.36,1);
  }

  .node--visible {
    opacity: 1;
    transform: translateY(0);
  }

  /* ── Meta (year + place) ────────────────────────────── */
  .node-meta {
    display: flex; flex-direction: column; gap: 0.2rem;
    padding-top: 0.2rem; text-align: right;
  }

  .node-year {
    font-family: var(--font-display);
    font-weight: 400; font-size: 0.95rem;
    color: var(--ink); letter-spacing: 0.02em;
  }

  .node-place {
    font-size: 0.62rem; font-weight: 300;
    letter-spacing: 0.08em; text-transform: uppercase;
    color: var(--ink-muted); line-height: 1.3;
  }

  /* ── Centre dot ─────────────────────────────────────── */
  .node-dot {
    display: flex; align-items: center; justify-content: center;
    width: 2.25rem; height: 2.25rem;
    border-radius: 50%;
    background: var(--linen-card);
    border: 1px solid var(--border);
    box-shadow: 0 2px 8px var(--shadow-warm);
    flex-shrink: 0;
    margin-top: 0.05rem;
    transition: box-shadow 0.3s;
  }

  .node--visible .node-dot {
    box-shadow: 0 4px 14px var(--shadow-warm);
  }

  .node-dot--question {
    background: var(--ink);
    border-color: var(--ink);
    animation: dot-pulse 2.8s ease-in-out infinite;
  }

  @keyframes dot-pulse {
    0%, 100% { box-shadow: 0 0 0 0 rgba(26,23,20,0.25); }
    50%       { box-shadow: 0 0 0 8px rgba(26,23,20,0); }
  }

  .node-icon {
    font-size: 0.65rem; color: var(--ink-muted);
    line-height: 1; user-select: none;
  }

  .node-dot--question .node-icon { color: #F0EBE3; font-size: 0.85rem; font-weight: 600; }

  /* ── Card ───────────────────────────────────────────── */
  .node-card {
    background: var(--linen-card);
    border: 1px solid var(--border-light);
    border-radius: 1.1rem;
    padding: 1.25rem 1.4rem 1.3rem;
    margin-bottom: 0;
    box-shadow: 0 2px 8px var(--shadow-warm);
    transition: box-shadow 0.3s, border-color 0.3s;
  }

  .node--visible .node-card {
    box-shadow: 0 4px 18px var(--shadow-warm);
  }

  .node-card--question {
    border-color: var(--border);
    background: linear-gradient(135deg, var(--linen-card) 0%, #F8F3EA 100%);
    position: relative; overflow: hidden;
  }

  /* ── Badge ──────────────────────────────────────────── */
  .card-badge-row {
    display: flex; align-items: center; gap: 0.5rem;
    margin-bottom: 0.55rem;
  }

  .badge {
    font-family: var(--font-display);
    font-weight: 500; font-size: 1.05rem;
    color: var(--ink); letter-spacing: 0.01em;
  }

  .badge-label {
    font-size: 0.62rem; font-weight: 300;
    letter-spacing: 0.12em; text-transform: uppercase;
    color: var(--ink-muted);
  }

  /* ── Card text ──────────────────────────────────────── */
  .card-title {
    font-family: var(--font-display);
    font-weight: 400; font-size: 1.2rem;
    color: var(--ink); margin: 0 0 0.5rem; line-height: 1.2;
  }

  .card-title--question {
    font-style: italic; color: var(--ink-mid);
  }

  .card-body {
    font-size: 0.8rem; font-weight: 300;
    line-height: 1.75; color: var(--ink-mid); margin: 0;
  }

  /* ── Decision fork ──────────────────────────────────── */
  .decision {
    margin-top: 1rem;
    padding-top: 0.85rem;
    border-top: 1px solid var(--border-light);
  }

  .decision-prompt {
    font-size: 0.62rem; font-weight: 300;
    letter-spacing: 0.14em; text-transform: uppercase;
    color: var(--ink-muted); margin: 0 0 0.6rem;
  }

  .options {
    display: flex; flex-wrap: wrap; gap: 0.4rem;
  }

  /* Base option pill */
  .option {
    display: inline-flex; align-items: center; gap: 0.3rem;
    border-radius: 999px;
    font-size: 0.68rem; font-weight: 400;
    letter-spacing: 0.04em;
    padding: 0.25rem 0.7rem;
    transition: opacity 0.2s;
  }

  /* Rejected: faded, warm strikethrough via text-decoration */
  .option--rejected {
    background: rgba(26,23,20,0.05);
    color: var(--ink-muted);
    text-decoration: line-through;
    text-decoration-color: rgba(154,143,131,0.5);
    text-decoration-thickness: 1px;
  }

  /* Chosen: same matte dark pill as home page */
  .option--chosen {
    background: var(--ink);
    color: #F0EBE3;
    box-shadow:
      inset 0 1px 0 rgba(255,255,255,0.10),
      inset 0 -1px 0 rgba(0,0,0,0.15),
      0 2px 8px rgba(0,0,0,0.16);
  }

  .option-note {
    font-style: italic; font-size: 0.6rem;
    opacity: 0.7; margin-left: 0.1rem;
  }

  .chosen-mark {
    font-size: 0.6rem; opacity: 0.65; margin-left: 0.1rem;
  }

  /* ── Question pulse glyph ───────────────────────────── */
  .question-pulse {
    position: absolute;
    top: 0.75rem; right: 1rem;
    font-family: var(--font-display);
    font-size: 5rem; font-weight: 300;
    color: rgba(26,23,20,0.04);
    line-height: 1;
    pointer-events: none;
    user-select: none;
    animation: q-breathe 4s ease-in-out infinite;
  }

  @keyframes q-breathe {
    0%, 100% { opacity: 1; }
    50%       { opacity: 0.35; }
  }

  /* ── Mobile ─────────────────────────────────────────── */
  @media (max-width: 500px) {
    .node {
      grid-template-columns: 3.8rem 1.9rem 1fr;
      gap: 0 0.75rem;
    }
    .node-dot { width: 1.9rem; height: 1.9rem; }
    .line-segment { margin-left: clamp(3rem, 15vw, 5rem); }
  }
</style>