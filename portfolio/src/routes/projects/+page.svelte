 <script>
  let expanded  = $state({});
  let imageOpen = $state({});
  let modalImage = $state();

  function toggle(title, e) {
    e.preventDefault();
    expanded[title] = !expanded[title];
    expanded = expanded;
  }

  function toggleImage(title, e) {
    e.preventDefault();
    e.stopPropagation();
    imageOpen[title] = !imageOpen[title];
  }

  function openModal(src, e) {
    e.preventDefault();
    e.stopPropagation();
    modalImage = src;
  }

  function closeModal() {
    modalImage = null;
  }

  /**
   * Color pairs: [pill-bg, dot-bg]
   * Each project gets a distinct matte dark color matching the home bubbles.
   */
  const projects = [
    {
      title: 'Master Thesis',
      date: '2025-2026',
      type: 'Research',
      typeColor: { bg: 'bg-blue-400/15', text: 'text-blue-700' },
      dotColor: '#2D3F4C',         // ocean slate
      orb: 'bg-blue-400',
      description:
        'Investigated how humans select words during speech by analyzing brain activity using novel machine learning techniques on real neural datasets using Python and MATLAB.  Conducted at <a href="https://diliberg.net/" target="_blank" rel="noopener noreferrer" class="underline hover:text-gray-700">DiLibERG Lab</a>, the project sits at the intersection of Neuroscience, Computer Science, Cognitive Science, and Psychology, applying computational methods to better understand language and cognition.'
    },
    {
      title: 'Multi-Page Web Scraper and PDF Generator',
      date: '2026',
      type: 'Software Project',
      typeColor: { bg: 'bg-orange-400/15', text: 'text-orange-700' },
      orb: 'bg-orange-400',
      description:
        'Built a Python tool that scrapes and extracts readable text from a given URL, designed for sequential content such as articles or book chapters. The system can follow multiple linked pages based on user input, aggregating and cleaning content by removing unwanted HTML elements and special characters. The extracted text is then formatted into a styled PDF with customizable output options. Implemented request-handling techniques to ensure stable and reliable data extraction while reducing the risk of bot detection.'
    },
    {
      title: 'Big Three vs Next Generation: Tennis Data Visualization',
      date: '2025',
      type: 'Visualization Project',
      typeColor: { bg: 'bg-orange-400/15', text: 'text-orange-700' },
      orb: 'bg-orange-400',
      image: "/images/dataviz.jpg",
      description:
        'Developed an interactive Python data visualization project analyzing and comparing the careers of the “Big Three” — Roger Federer, Rafael Nadal, and Novak Djokovic — with emerging players Jannik Sinner and Carlos Alcaraz. Used multiple visualization techniques, including timeline comparisons and statistical graphs, to identify career trends, compare early-career progression, and analyze player strengths and performance patterns.'
    },
    {
      title: 'Hackathon GenAI x Law - MVP Bonus Prize',
      date: '2024',
      type: 'Competition',
      typeColor: { bg: 'bg-purple-400/15', text: 'text-purple-700' },
      orb: 'bg-purple-400',
      image: 'images/hacktrinity.jpg',
      description:
        'Built a 48-hour hackathon project at HackTrinity in a team of four: a court hearing summarizer with outcome prediction using NLP and classification, awarded MVP bonus prize. Developed using React and Python with integration of the Perplexity API for intelligent data processing and summarization.'
    },
    {
      title: 'Computer Vision Project',
      date: '2024',
      type: 'System',
      typeColor: { bg: 'bg-orange-400/15', text: 'text-orange-700' },
      orb: 'bg-orange-400',
      image: 'images/crossings.png',
      description:
        'Built a system in C++ that analyzes images to detect pedestrian crossings and visually identify their locations. The model was evaluated against ground truth datasets using precision and recall metrics to measure detection accuracy and assess false positives. The system achieved strong performance on standard and distance-perspective crossing scenarios.'
    },
    {
      title: 'Paper about AI Ethics',
      date: '2024',
      type: 'Research',
      typeColor: { bg: 'bg-blue-400/15', text: 'text-blue-700' },
      orb: 'bg-blue-400',
      image: 'images/ethicspaper.png',
      description:
        'Explored ethical considerations of algorithmic fairness in artificial intelligence by investigating different types of bias and their impact on model outcomes. Used a real-world inspired dataset to train a predictive model estimating the likelihood of student dropout based on multiple socio-academic factors. Analyzed how bias in data and model design can influence predictions and lead to inequitable outcomes.'
    },
    {
      title: 'Air Quality Monitoring and Trend Analysis System',
      date: '2024',
      type: 'Software / System',
      typeColor: { bg: 'bg-orange-400/15', text: 'text-orange-700' },
      orb: 'bg-orange-400',
      description:
        'Developed a C++ application structured using the Model-View-Controller (MVC) design pattern. Built collaboratively in a team of three, the project focused on designing algorithms to efficiently retrieve and process data from monitoring systems tracking both private and public air pollution sources. The application was used to analyze environmental data and identify pollution trends over time.'
    },
    {
      title: 'Digital Student–Teacher Interaction System',
      date: '2024',
      type: 'Software / System',
      typeColor: { bg: 'bg-orange-400/15', text: 'text-orange-700' },
      orb: 'bg-orange-400',
      description:
        'Developed a full-stack Java application using Spring Boot as part of a three-person team. The system supported two user roles: students and teachers. Students could view their grades across subjects and request video calls with teachers based on availability. Teachers had access to a scheduling calendar, upcoming sessions, and performance analytics related to student grades.'
    },
    // ... rest of your projects
  ];
</script>

<!-- Image modal -->
{#if modalImage}
  <div
    class="modal-backdrop"
    onclick={closeModal}
    role="dialog"
    aria-modal="true"
  >
    <img
      src={modalImage}
      alt="Project preview"
      class="modal-img"
      onclick={(e) => e.stopPropagation()}
    />
  </div>
{/if}

<div class="page">

  <!-- Grain overlay — same as home -->
  <div class="grain" aria-hidden="true"></div>

  <!-- Warm ambient washes -->
  <div class="ambient ambient--tl" aria-hidden="true"></div>
  <div class="ambient ambient--br" aria-hidden="true"></div>

  <div class="inner">

    <!-- Page header -->
    <header class="page-header">
      <p class="eyebrow">Selected work</p>
      <h1 class="page-title">Projects</h1>
      <div class="rule"></div>
    </header>

    <!-- Card grid -->
    <ul class="grid" role="list">
      {#each projects as project (project.title)}
        <li>
          <!-- svelte-ignore a11y_no_noninteractive_element_interactions -->
          <article
            class="card"
            class:card--expanded={expanded[project.title]}
            onclick={(e) => toggle(project.title, e)}
            onkeydown={(e) => e.key === 'Enter' && toggle(project.title, e)}
            tabindex="0"
            role="button"
            aria-expanded={expanded[project.title] ?? false}
          >

            <!-- Top row: tags + optional image toggle -->
            <div class="card-tags">
              <span class="tag tag--date">{project.date}</span>
              <span class="tag text-[11px] font-medium {project.typeColor.bg} ">{project.type}</span>

              {#if project.image}
                <button
                  class="img-toggle"
                  onclick={(e) => toggleImage(project.title, e)}
                  aria-label={imageOpen[project.title] ? 'Hide preview' : 'Show preview'}
                >
                  {#if imageOpen[project.title]}
                    <!-- eye-off -->
                    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                      <path d="M17.94 17.94A10.07 10.07 0 0 1 12 20c-7 0-11-8-11-8a18.45 18.45 0 0 1 5.06-5.94"/>
                      <path d="M9.9 4.24A9.12 9.12 0 0 1 12 4c7 0 11 8 11 8a18.5 18.5 0 0 1-2.16 3.19"/>
                      <line x1="1" y1="1" x2="23" y2="23"/>
                    </svg>
                  {:else}
                    <!-- eye -->
                    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                      <path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"/>
                      <circle cx="12" cy="12" r="3"/>
                    </svg>
                  {/if}
                </button>
              {/if}

              <!-- Matte accent dot (replaces colored orb blob) -->
              <span
                class="accent-dot"
                aria-hidden="true"
                style="background: {project.dotColor};"
              ></span>
            </div>

            <!-- Image reveal -->
            {#if project.image}
              <div class="img-wrap" class:img-wrap--open={imageOpen[project.title]}>
                <img
                  src={project.image}
                  alt="{project.title} preview"
                  class="preview-img"
                  onclick={(e) => openModal(project.image, e)}
                />
              </div>
            {/if}

            <!-- Title -->
            <h2 class="card-title">{project.title}</h2>

            <!-- Description -->
            <p
              class="card-desc"
              class:card-desc--clamped={!expanded[project.title]}
            >
              {@html project.description}
            </p>

            {#if !expanded[project.title]}
              <span class="expand-hint" aria-hidden="true">tap to read more</span>
            {/if}

          </article>
        </li>
      {/each}
    </ul>

  </div>
</div>

<style>
  /* ── Page shell ───────────────────────────────────────── */
  .page {
    position: relative;
    min-height: 100svh;
    overflow: hidden;
    background: var(--linen);
    padding: 4rem 1.5rem 5rem;
  }

  /* Grain — matches home page */
  .grain {
    position: absolute;
    inset: 0;
    pointer-events: none;
    z-index: 1;
    opacity: 0.045;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
    background-size: 180px 180px;
  }

  /* Ambient washes — no coloured blobs */
  .ambient {
    position: absolute;
    pointer-events: none;
    z-index: 0;
    border-radius: 50%;
  }
  .ambient--tl {
    top: -8rem; left: -8rem;
    width: 32rem; height: 32rem;
    background: radial-gradient(ellipse, rgba(180,160,130,0.14) 0%, transparent 70%);
  }
  .ambient--br {
    bottom: -6rem; right: -6rem;
    width: 26rem; height: 26rem;
    background: radial-gradient(ellipse, rgba(120,100,80,0.10) 0%, transparent 70%);
  }

  /* ── Inner container ──────────────────────────────────── */
  .inner {
    position: relative;
    z-index: 10;
    max-width: 64rem;
    margin: 0 auto;
  }

  /* ── Page header ──────────────────────────────────────── */
  .page-header {
    margin-bottom: 3rem;
  }

  .eyebrow {
    font-family: var(--font-body);
    font-weight: 300;
    font-size: 0.7rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--ink-muted);
    margin: 0 0 0.5rem;
  }

  .page-title {
    font-family: var(--font-display);
    font-weight: 300;
    font-size: clamp(2.4rem, 5vw, 4rem);
    letter-spacing: -0.01em;
    color: var(--ink);
    margin: 0 0 1rem;
    line-height: 1;
  }

  .rule {
    width: 2.5rem;
    height: 1px;
    background: var(--border);
  }

  /* ── Grid ─────────────────────────────────────────────── */
  .grid {
    list-style: none;
    margin: 0;
    padding: 0;
    display: grid;
    grid-template-columns: 1fr;
    gap: 1rem;
  }

  @media (min-width: 640px)  { .grid { grid-template-columns: repeat(2, 1fr); } }
  @media (min-width: 1024px) { .grid { grid-template-columns: repeat(3, 1fr); } }

  /* ── Card ─────────────────────────────────────────────── */
  .card {
    position: relative;
    display: flex;
    flex-direction: column;
    height: 100%;
    background: var(--linen-card);
    border: 1px solid var(--border-light);
    border-radius: 1.25rem;
    padding: 1.25rem;
    cursor: pointer;
    transition:
      transform 0.25s cubic-bezier(0.34, 1.56, 0.64, 1),
      box-shadow 0.25s ease,
      border-color 0.2s;
    box-shadow: 0 2px 8px var(--shadow-warm), 0 1px 2px rgba(30,20,10,0.05);
    /* Matte feel — no backdrop blur needed on cards */
  }

  .card:hover,
  .card:focus-visible {
    transform: translateY(-3px);
    box-shadow: 0 8px 28px var(--shadow-warm), 0 2px 6px rgba(30,20,10,0.08);
    border-color: var(--border);
    outline: none;
  }

  .card:focus-visible {
    outline: 2px solid var(--ink-muted);
    outline-offset: 2px;
  }

  /* ── Tags row ─────────────────────────────────────────── */
  .card-tags {
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    gap: 0.4rem;
    margin-bottom: 0.75rem;
  }

  .tag {
    border-radius: 999px;
    font-size: 0.65rem;
    font-weight: 400;
    letter-spacing: 0.06em;
    padding: 0.2rem 0.65rem;
  }

  .tag--date {
    background: rgba(26, 23, 20, 0.06);
    color: var(--ink-muted);
  }



  /* Matte accent dot — replaces coloured orb blobs */
  .accent-dot {
    display: block;
    width: 8px;
    height: 8px;
    border-radius: 50%;
    margin-left: auto;
    flex-shrink: 0;
    box-shadow: inset 0 1px 0 rgba(255,255,255,0.12), 0 1px 3px rgba(0,0,0,0.25);
  }

  /* ── Image toggle button ──────────────────────────────── */
  .img-toggle {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 1.5rem;
    height: 1.5rem;
    border-radius: 50%;
    border: 1px solid var(--border);
    background: transparent;
    color: var(--ink-muted);
    cursor: pointer;
    transition: background 0.2s, color 0.2s;
    padding: 0;
  }

  .img-toggle:hover {
    background: rgba(26, 23, 20, 0.07);
    color: var(--ink);
  }

  .img-toggle svg {
    width: 0.8rem;
    height: 0.8rem;
  }

  /* ── Image reveal ─────────────────────────────────────── */
  .img-wrap {
    overflow: hidden;
    max-height: 0;
    opacity: 0;
    border-radius: 0.75rem;
    margin-bottom: 0;
    transition: max-height 0.4s ease, opacity 0.35s ease, margin-bottom 0.3s ease;
  }

  .img-wrap--open {
    max-height: 12rem;
    opacity: 1;
    margin-bottom: 0.75rem;
  }

  .preview-img {
    width: 100%;
    height: 12rem;
    object-fit: cover;
    border-radius: 0.75rem;
    cursor: zoom-in;
  }

  /* ── Card body ────────────────────────────────────────── */
  .card-title {
    font-family: var(--font-display);
    font-weight: 400;
    font-size: 1.05rem;
    line-height: 1.3;
    color: var(--ink);
    margin: 0 0 0.5rem;
  }

  .card-desc {
    flex: 1;
    font-size: 0.78rem;
    line-height: 1.7;
    color: var(--ink-mid);
    font-weight: 300;
    margin: 0;
    text-align: justify;
  }

  .card-desc--clamped {
    display: -webkit-box;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }

  .expand-hint {
    display: block;
    margin-top: 0.5rem;
    font-size: 0.65rem;
    letter-spacing: 0.08em;
    color: var(--ink-muted);
    user-select: none;
  }

  /* ── Modal ────────────────────────────────────────────── */
  .modal-backdrop {
    position: fixed;
    inset: 0;
    z-index: 100;
    display: flex;
    align-items: center;
    justify-content: center;
    background: rgba(26, 23, 20, 0.55);
    backdrop-filter: blur(6px);
    border: none;
    cursor: zoom-out;
  }

  .modal-img {
    max-height: 80vh;
    max-width: 90vw;
    border-radius: 1rem;
    box-shadow: 0 32px 80px rgba(0,0,0,0.35);
    cursor: auto;
  }
</style>
