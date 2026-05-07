<script>
  const projects = [
    {
      title: 'Master Thesis',
      date: '2025-2026',
      type: 'Research',
      typeColor: { bg: 'bg-blue-400/15', text: 'text-blue-700' },
      orb: 'bg-blue-400',
      description:
        'Investigating how humans choose words during speech by analyzing brain activity with novel machine learning techniques.'
    },
    {
      title: 'Computer Vision Project',
      date: '2024',
      type: 'System',
      typeColor: { bg: 'bg-orange-400/15', text: 'text-orange-700' },
      orb: 'bg-orange-400',
      description:
        'Built a system that analyzes images to detect pedestrian crossings and visually indicate their position.'
    },
    {
      title: 'Paper about AI Ethics',
      date: '2024',
      type: 'Research',
      typeColor: { bg: 'bg-blue-400/15', text: 'text-blue-700' },
      orb: 'bg-blue-400',
      description:
        'Ethical Explorations of Algorithmic Equity in Artificial Intelligence'
    },
    // ... rest of your projects
  ];
</script>

<div class="relative min-h-screen overflow-clip bg-white px-6 py-20">
  <!-- Gradient blobs -->
  <div aria-hidden="true" class="pointer-events-none absolute -left-32 -top-32 h-[28rem] w-[28rem] rounded-full bg-blue-200/50 blur-3xl"></div>
  <div aria-hidden="true" class="pointer-events-none absolute -bottom-20 -right-32 h-[28rem] w-[28rem] rounded-full bg-pink-200/50 blur-3xl"></div>
  <div aria-hidden="true" class="pointer-events-none absolute bottom-20 left-1/3 h-72 w-72 rounded-full bg-green-200/40 blur-3xl"></div>
  <div aria-hidden="true" class="pointer-events-none absolute right-1/4 top-20 h-64 w-64 rounded-full bg-amber-200/35 blur-3xl"></div>

  <div class="relative z-10 mx-auto max-w-5xl">
    <!-- Page header -->
    <header class="mb-14">
      <p class="mb-1 text-xs font-medium uppercase tracking-widest text-gray-400">
        Selected work
      </p>
      <h1 class="text-4xl font-semibold tracking-tight text-gray-800 sm:text-5xl">
        Projects
      </h1>
    </header>

    <!-- Card grid -->
    <ul class="grid grid-cols-1 gap-5 sm:grid-cols-2 lg:grid-cols-3" role="list">
      {#each projects as project (project.title)}
        <li>
          <a
            href={project.href}
            class="group relative flex h-full flex-col overflow-hidden rounded-3xl border border-white/80 bg-white/55 p-6 shadow-md shadow-black/5 backdrop-blur-xl transition-all duration-300 ease-out hover:-translate-y-1.5 hover:bg-white/75 hover:shadow-xl hover:shadow-black/10 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-gray-400/60 focus-visible:ring-offset-2"
          >
            <!-- Decorative orb -->
            <div
              aria-hidden="true"
              class="absolute -right-5 -top-5 h-20 w-20 rounded-full {project.orb} opacity-30 blur-xl transition-opacity duration-300 group-hover:opacity-50"
            ></div>

            <!-- Inner highlight ring -->
            <div
              aria-hidden="true"
              class="pointer-events-none absolute inset-0 rounded-3xl ring-1 ring-inset ring-white/60"
            ></div>

            <!-- Tags -->
            <div class="relative mb-3 flex items-center gap-2">
              <span class="rounded-full bg-black/[0.06] px-2.5 py-0.5 text-[11px] font-medium text-black/40">
                {project.date}
              </span>
              <span class="rounded-full px-2.5 py-0.5 text-[11px] font-medium {project.typeColor.bg} {project.typeColor.text}">
                {project.type}
              </span>
            </div>

            <!-- Title -->
            <h2 class="relative mb-2 text-base font-semibold leading-snug text-gray-800 sm:text-[15px]">
              {project.title}
            </h2>

            <!-- Description -->
            <p class="relative line-clamp-3 flex-1 text-[13px] leading-relaxed text-gray-500">
              {project.description}
            </p>

            <!-- Footer arrow -->
            <div class="relative mt-6 flex justify-end">
              <span
                aria-hidden="true"
                class="flex h-7 w-7 items-center justify-center rounded-full border border-black/[0.07] bg-black/[0.04] text-sm text-black/30 transition-all duration-200 group-hover:bg-black/[0.08] group-hover:text-black/60 group-hover:translate-x-0.5"
              >
                →
              </span>
            </div>
          </a>
        </li>
      {/each}
    </ul>
  </div>
</div>