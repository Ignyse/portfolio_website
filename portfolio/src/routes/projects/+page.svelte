<script>
  let expanded = $state({});
  let imageOpen = $state({});
  let modalImage =  $state();
  function toggle(title, e) {
    e.preventDefault(); // prevent navigation on expand
    expanded[title] = !expanded[title];
    expanded = expanded; // trigger reactivity
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

  const projects = [
    {
      title: 'Master Thesis',
      date: '2025-2026',
      type: 'Research',
      typeColor: { bg: 'bg-blue-400/15', text: 'text-blue-700' },
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
    
    {#if modalImage}
  <div
    class="fixed inset-0 z-50 flex items-center justify-center bg-black/60 backdrop-blur-sm"
    onclick={closeModal}
    role="dialog"
    aria-modal="true"
  >
    <img
      src={modalImage}
      alt="Project preview"
      class="max-h-[80vh] max-w-[90vw] rounded-2xl shadow-2xl"
      onclick={(e) => e.stopPropagation()}
    />
  </div>
{/if}

    <!-- Card grid -->
    <ul class="grid grid-cols-1 gap-5 sm:grid-cols-2 lg:grid-cols-3" role="list">
      {#each projects as project (project.title)}
        <li>
          <a
            href={project.href}
            class="group relative flex h-full flex-col overflow-hidden rounded-3xl border border-white/80 bg-white/55 p-6 shadow-md shadow-black/5 backdrop-blur-xl transition-all duration-300 ease-out hover:-translate-y-1.5 hover:bg-white/75 hover:shadow-xl hover:shadow-black/10 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-gray-400/60 focus-visible:ring-offset-2"
            onclick={(e) => toggle(project.title, e)}
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
             <!-- Image toggle icon — only if project has an image -->
          {#if project.image}
            <button
              onclick={(e) => toggleImage(project.title, e)}
              class="ml-auto flex h-6 w-6 items-center justify-center rounded-full border border-black/[0.08] bg-black/[0.04] text-black/30 transition-all duration-200 hover:bg-black/[0.09] hover:text-black/60"
              aria-label="Toggle project preview"
            >
              <!-- Eye icon -->
              {#if imageOpen[project.title]}
                <svg xmlns="http://www.w3.org/2000/svg" class="h-3.5 w-3.5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                  <path d="M17.94 17.94A10.07 10.07 0 0 1 12 20c-7 0-11-8-11-8a18.45 18.45 0 0 1 5.06-5.94"/>
                  <path d="M9.9 4.24A9.12 9.12 0 0 1 12 4c7 0 11 8 11 8a18.5 18.5 0 0 1-2.16 3.19"/>
                  <line x1="1" y1="1" x2="23" y2="23"/>
                </svg>
              {:else}
                <svg xmlns="http://www.w3.org/2000/svg" class="h-3.5 w-3.5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                  <path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"/>
                  <circle cx="12" cy="12" r="3"/>
                </svg>
              {/if}
            </button>
          {/if}

        <!-- Optional image preview -->
        {#if project.image}
          <div
            class="relative mb-3 overflow-hidden rounded-2xl transition-all duration-500 ease-in-out {imageOpen[project.title] ? 'max-h-48 opacity-100' : 'max-h-0 opacity-0'}"
          >
            <img
              src={project.image}
              alt="{project.title} preview"
              onclick={(e) => openModal(project.image, e)}
              class="h-48 w-full object-cover"
            />
          </div>
        {/if}

            <!-- Title -->
            <h2 class="relative mb-2 text-base font-semibold leading-snug text-gray-800 sm:text-[15px]">
              {project.title}
            </h2>

            <!-- Description -->
            <p class="relative flex-1 text-[13px] leading-relaxed text-justify text-gray-500 {expanded[project.title] ? '' : 'line-clamp-3'}">
              {@html project.description}
            </p>

              <!-- Expand hint -->
        {#if !expanded[project.title]}
          <span class="relative mt-2 text-[11px] text-black/30 select-none">tap to read more</span>
        {/if}
          </a>
        </li>
      {/each}
    </ul>
  </div>
</div>