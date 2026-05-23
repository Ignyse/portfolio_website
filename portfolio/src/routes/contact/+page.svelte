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
    ]

  let copied = $state(false);

  async function copyEmail(e) {
    e.preventDefault();
    await navigator.clipboard.writeText(email);
    copied = true;
    setTimeout(() => (copied = false), 2000);
  }
</script>

<div class="page">

  <!-- Grain — same as home/projects -->
  <div class="grain" aria-hidden="true"></div>

  <!-- Ambient washes -->
  <div class="ambient ambient--top"    aria-hidden="true"></div>
  <div class="ambient ambient--bottom" aria-hidden="true"></div>

  <div class="inner">

    <!-- Page header -->
    <header class="page-header">
      <p class="eyebrow">Get in touch</p>

      <!-- Cormorant italic for the quote — editorial weight -->
      <h1 class="page-quote">
        What arrives by chance becomes<br />
        <em>opportunity</em> for the one who is open.
      </h1>

      <div class="rule"></div>
    </header>

    <div class="sections">

      <!-- Email ──────────────────────────────────────────── -->
      <section class="section">
        <p class="section-label">Email</p>

        <div class="email-row">
          <a href="mailto:{email}" class="email-link">{email}</a>

          <!-- Subtle copy button -->
          <button
            class="copy-btn"
            class:copy-btn--done={copied}
            onclick={copyEmail}
            aria-label="Copy email address"
            title={copied ? 'Copied!' : 'Copy'}
          >
            {#if copied}
              <!-- checkmark -->
              <svg viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <polyline points="2 8 6 12 14 4"/>
              </svg>
            {:else}
              <!-- copy icon -->
              <svg viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round">
                <rect x="5" y="5" width="8" height="8" rx="1.5"/>
                <path d="M11 5V3.5A1.5 1.5 0 0 0 9.5 2h-6A1.5 1.5 0 0 0 2 3.5v6A1.5 1.5 0 0 0 3.5 11H5"/>
              </svg>
            {/if}
          </button>
        </div>
      </section>

      <!-- Socials ─────────────────────────────────────────── -->
      <section class="section">
        <p class="section-label">Elsewhere</p>

        <div class="social-row">
          {#each socials as social}
            <a
              href={social.url}
              target="_blank"
              rel="noopener noreferrer"
              class="social-pill"
            >
              {social.name}
              <!-- External arrow -->
              <svg class="social-arrow" viewBox="0 0 12 12" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
                <path d="M2 10 L10 2 M5 2 h5 v5"/>
              </svg>
            </a>
          {/each}
        </div>
      </section>

      <!-- Closing ─────────────────────────────────────────── -->
      <section class="closing">
        <p>
          Interested in building from scratch — open to startups, collaborations,
          full-time roles, freelance projects, and conversations with ambitious builders.
        </p>
      </section>

    </div>
  </div>
</div>

<style>
  /* ── Page shell ───────────────────────────────────────── */
  .page {
    position: relative;
    min-height: 100svh;
    overflow: hidden;
    background: var(--linen);
    padding: 5rem 1.5rem 6rem;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  /* Grain */
  .grain {
    position: absolute;
    inset: 0;
    pointer-events: none;
    z-index: 1;
    opacity: 0.045;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
    background-size: 180px 180px;
  }

  /* Ambient */
  .ambient {
    position: absolute;
    pointer-events: none;
    z-index: 0;
    border-radius: 50%;
  }
  .ambient--top {
    top: -10%; left: 50%;
    transform: translateX(-50%);
    width: 50vw; height: 40vh;
    background: radial-gradient(ellipse, rgba(180,160,130,0.16) 0%, transparent 70%);
  }
  .ambient--bottom {
    bottom: -8%; left: 50%;
    transform: translateX(-50%);
    width: 36vw; height: 30vh;
    background: radial-gradient(ellipse, rgba(120,100,80,0.10) 0%, transparent 70%);
  }

  /* ── Inner ────────────────────────────────────────────── */
  .inner {
    position: relative;
    z-index: 10;
    width: 100%;
    max-width: 38rem;
    margin: 0 auto;
  }

  /* ── Page header ──────────────────────────────────────── */
  .page-header {
    margin-bottom: 3.5rem;
    text-align: center;
  }

  .eyebrow {
    font-family: var(--font-body);
    font-weight: 300;
    font-size: 0.7rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--ink-muted);
    margin: 0 0 1rem;
  }

  .page-quote {
    font-family: var(--font-display);
    font-weight: 300;
    font-size: clamp(1.7rem, 4.5vw, 2.8rem);
    line-height: 1.25;
    letter-spacing: -0.01em;
    color: var(--ink);
    margin: 0 0 1.5rem;
  }

  /* italic sits inside Cormorant — naturally elegant */
  .page-quote em {
    font-style: italic;
    font-weight: 300;
    color: var(--ink-mid);
  }

  .rule {
    width: 2.5rem;
    height: 1px;
    background: var(--border);
    margin: 0 auto;
  }

  /* ── Sections ─────────────────────────────────────────── */
  .sections {
    display: flex;
    flex-direction: column;
    gap: 2.5rem;
  }

  .section {
    text-align: center;
  }

  .section-label {
    font-family: var(--font-body);
    font-weight: 300;
    font-size: 0.68rem;
    letter-spacing: 0.18em;
    text-transform: uppercase;
    color: var(--ink-muted);
    margin: 0 0 0.85rem;
  }

  /* ── Email ────────────────────────────────────────────── */
  .email-row {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0.75rem;
    flex-wrap: wrap;
  }

  .email-link {
    font-family: var(--font-display);
    font-weight: 400;
    font-size: clamp(1.4rem, 3.5vw, 2.2rem);
    letter-spacing: -0.01em;
    color: var(--ink);
    text-decoration: none;
    border-bottom: 1px solid var(--border);
    transition: color 0.2s, border-color 0.2s;
  }

  .email-link:hover {
    color: var(--ink-mid);
    border-color: var(--ink-mid);
  }

  .copy-btn {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 1.9rem;
    height: 1.9rem;
    border-radius: 50%;
    border: 1px solid var(--border);
    background: var(--linen-card);
    color: var(--ink-muted);
    cursor: pointer;
    transition: background 0.2s, color 0.2s, border-color 0.2s;
    padding: 0;
    flex-shrink: 0;
  }

  .copy-btn:hover {
    background: rgba(26,23,20,0.07);
    color: var(--ink);
    border-color: var(--border);
  }

  .copy-btn--done {
    background: #1E3A2F;
    color: #d4ead8;
    border-color: #1E3A2F;
  }

  .copy-btn svg {
    width: 0.85rem;
    height: 0.85rem;
  }

  /* ── Socials ──────────────────────────────────────────── */
  .social-row {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 0.6rem;
  }

  .social-pill {
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
    padding: 0.55rem 1.2rem;
    border-radius: 999px;
    background: var(--ink);          /* same dark matte as home pills */
    color: #F0EBE3;
    font-family: var(--font-body);
    font-weight: 400;
    font-size: 0.82rem;
    letter-spacing: 0.05em;
    text-decoration: none;
    box-shadow:
      inset 0 1px 0 rgba(255,255,255,0.10),
      inset 0 -1px 0 rgba(0,0,0,0.15),
      0 2px 8px rgba(0,0,0,0.18);
    transition: transform 0.22s cubic-bezier(0.34,1.56,0.64,1), box-shadow 0.2s;
  }

  .social-pill:hover {
    transform: translateY(-2px) scale(1.04);
    box-shadow:
      inset 0 1px 0 rgba(255,255,255,0.13),
      inset 0 -1px 0 rgba(0,0,0,0.2),
      0 6px 18px rgba(0,0,0,0.22);
  }

  .social-arrow {
    width: 0.7rem;
    height: 0.7rem;
    opacity: 0.6;
  }

  /* ── Closing ──────────────────────────────────────────── */
  .closing {
    padding-top: 2rem;
    border-top: 1px solid var(--border-light);
    text-align: center;
  }

  .closing p {
    font-size: 0.82rem;
    line-height: 1.75;
    color: var(--ink-muted);
    font-weight: 300;
    max-width: 30rem;
    margin: 0 auto;
  }
</style>
