<script>
  const interests = [
    {
      label: 'Composing Music',
      glass: 'bg-blue-400/25 border-blue-200/50 hover:bg-blue-400/45',
      blob: 'bg-blue-200/60',
      ring: 'focus-visible:ring-blue-300/70',
      x: -22, y: -17,
      delay: '0s',
      description: 'Classically trained in violin, I enjoy creating my own melodies and turning ideas into music.',
    },
    {
      label: 'Water Sports',
      glass: 'bg-cyan-400/25 border-cyan-200/50 hover:bg-cyan-400/45',
      blob: 'bg-cyan-200/60',
      ring: 'focus-visible:ring-cyan-300/70',
      x: 24, y: -15,
      delay: '0.7s',
      description: 'I started swimming later than most, but by 10 I had completed a 1 km lake marathon, and by 12 I had won my first solo sailing competition.',
    },
    {
      label: 'Languages',
      glass: 'bg-pink-400/25 border-pink-200/50 hover:bg-pink-400/45',
      blob: 'bg-pink-200/60',
      ring: 'focus-visible:ring-pink-300/70',
      x: -26, y: 20,
      delay: '1.4s',
      description: "I learned French at six, and I'm currently challenging myself to learn 한국어.",
    },
    {
      label: 'Coding',
      glass: 'bg-green-400/25 border-green-200/50 hover:bg-green-400/45',
      blob: 'bg-green-200/60',
      ring: 'focus-visible:ring-green-300/70',
      x: 25, y: 22,
      delay: '2.1s',
      description: 'I chose Computer Science to turn logic and creativity into tools that could help people and spark imagination.',
    },
    {
      label: 'Photography',
      glass: 'bg-amber-400/25 border-amber-200/50 hover:bg-amber-400/45',
      blob: 'bg-amber-200/60',
      ring: 'focus-visible:ring-amber-300/70',
      x: 0, y: -30,
      delay: '2.8s',
      description: "I'm drawn to nature and animal photography for the detail, calm, and stories found in small moments.",
    },
    {
      label: 'Motivation',
      glass: 'bg-orange-400/25 border-orange-200/50 hover:bg-orange-400/45',
      blob: 'bg-orange-200/60',
      ring: 'focus-visible:ring-amber-300/70',
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

<!--
  overflow-clip clips paint without creating a scroll container,
  preventing edge-bubble clipping from appearing as a scrollbar.
-->
<div class="relative h-screen flex items-center justify-center overflow-clip bg-white">

  <!-- Ambient gradient blobs — these are what the glass effect refracts -->
  {#each interests as item (item.label)}
    <div
      aria-hidden="true"
      class="blob absolute rounded-full blur-3xl pointer-events-none {item.blob}"
      style="
        width: 28rem; height: 28rem;
        left: clamp(0%, calc(50% + {item.x}%), 100%);
        top:  clamp(0%, calc(50% + {item.y}%), 100%);
        transform: translate(-50%, -50%);
        animation: drift {4 + Math.abs(item.x % 3)}s ease-in-out infinite;
        animation-delay: {item.delay};
      "
    ></div>
  {/each}

  <!-- Subtle centre glow so the hero text pops -->
  <div
    aria-hidden="true"
    class="absolute w-64 h-64 rounded-full bg-white/80 blur-2xl pointer-events-none"
    style="top: 50%; left: 50%; transform: translate(-50%, -50%);"
  ></div>

  <!-- Click-outside dismissal — real <button>, no a11y warnings -->
  {#if selected}
    <button
      type="button"
      aria-label="Dismiss tooltip"
      class="absolute inset-0 z-10 cursor-default bg-transparent"
      onclick={() => (selected = null)}
    ></button>
  {/if}

  <!-- Hero text -->
  <div class="z-20 text-center px-4 pointer-events-none select-none">
    <h1 class="text-4xl sm:text-6xl font-semibold text-gray-800 tracking-tight mb-2">
      Ignacy Sus
    </h1>
    <p class="text-gray-400 text-base sm:text-lg tracking-wide">
      Creative Technologist
    </p>
  </div>

  <!-- Bubbles -->
  {#each interests as item (item.label)}
    <div
      class="absolute z-20"
      style="
        left: clamp(14%, calc(50% + {item.x}%), 86%);
        top:  clamp(13%, calc(50% + {item.y}%), 87%);
        transform: translate(-50%, -50%);
      "
    >
      <!-- Float wrapper — owns ONLY translateY; isolated from button's scale -->
      <div class="floating" style="animation-delay: {item.delay};">

        <!-- Tooltip -->
        {#if selected?.label === item.label}
          <div
            role="tooltip"
            id="tip-{item.label.replace(/\s+/g, '-')}"
            class="
              absolute bottom-full mb-3 left-1/2 -translate-x-1/2
              bg-white/75 backdrop-blur-md
              border border-white/60
              text-gray-600 text-xs sm:text-sm rounded-2xl
              px-4 py-2.5 w-max max-w-[190px] text-center
              shadow-xl pointer-events-none
            "
          >
            {item.description}
            <!-- Caret -->
            <span
              aria-hidden="true"
              class="absolute top-full left-1/2 -translate-x-1/2
                     border-[5px] border-transparent border-t-white/75"
            ></span>
          </div>
        {/if}

        <!-- The bubble -->
        <button
          type="button"
          aria-pressed={selected?.label === item.label}
          aria-describedby={selected?.label === item.label
            ? `tip-${item.label.replace(/\s+/g, '-')}`
            : undefined}
          onclick={(e) => { e.stopPropagation(); toggle(item); }}
          class="
            {item.glass} {item.ring}
            {selected?.label === item.label
              ? 'scale-110 shadow-2xl border-white/70 bg-opacity-50'
              : 'shadow-lg'}
            backdrop-blur-md border
            text-white font-medium tracking-wide
            flex items-center justify-center gap-1
            rounded-full whitespace-nowrap cursor-pointer
            px-4 sm:px-6
            h-9 sm:h-14
            text-[11px] sm:text-sm md:text-base
            max-w-[130px] sm:max-w-[230px]
            ring-1 ring-inset ring-white/30
            transition-all duration-300 ease-out
            hover:scale-110 hover:shadow-2xl hover:border-white/70
            focus-visible:outline-none focus-visible:ring-2
            focus-visible:ring-offset-2 focus-visible:ring-offset-transparent
            active:scale-95
          "
        >
          <span class="truncate" style="text-shadow: 0 1px 3px rgba(0,0,0,0.2);">
            {item.label}
          </span>
        </button>

      </div>
    </div>
  {/each}
</div>

<style>
  /* Float — lives on its own element, never conflicts with button's scale */
  .floating {
    animation: float 4s ease-in-out infinite;
  }

  @keyframes float {
    0%, 100% { transform: translateY(0px); }
    50%       { transform: translateY(-10px); }
  }

  /* Blobs drift very slowly — gives the background life */
  @keyframes drift {
    0%, 100% { transform: translate(-50%, -50%) scale(1); }
    50%       { transform: translate(-50%, -52%) scale(1.05); }
  }
</style>