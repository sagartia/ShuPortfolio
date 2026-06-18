<script setup>
import {
  ArrowRight,
  Calendar,
  ChevronDown,
  Cloud,
  Code2,
  Database,
  ExternalLink,
  Layers,
  Mail,
  MapPin,
  Menu,
  Moon,
  Server,
  Sun,
  Terminal,
  Zap,
} from 'lucide-vue-next'
import { ref, watch, onMounted, onUnmounted } from 'vue'

const navItems = [
  { label: 'about', href: '#about' },
  { label: 'projects', href: '#projects' },
  { label: 'experience', href: '#experience' },
  { label: 'contact', href: '#contact' },
]

const scrolled = ref(false)
const onScroll = () => { scrolled.value = window.scrollY > 10 }
onMounted(() => window.addEventListener('scroll', onScroll))
onUnmounted(() => window.removeEventListener('scroll', onScroll))

const isDark = ref(
  localStorage.getItem('theme') === 'dark' ||
  (!localStorage.getItem('theme') && window.matchMedia('(prefers-color-scheme: dark)').matches)
)
watch(isDark, (val) => {
  document.documentElement.classList.toggle('dark', val)
  localStorage.setItem('theme', val ? 'dark' : 'light')
}, { immediate: true })

const skillGroups = ref([
  {
    title: 'Backend',
    icon: Server,
    skills: ['Java', 'Spring Boot', 'Node.js', 'Go', 'Python', 'RESTful API', 'GraphQL', 'Microservices'],
  },
  {
    title: 'Frontend',
    icon: Code2,
    skills: ['React', 'TypeScript', 'Next.js', 'Tailwind CSS', 'Vue.js', 'Vite'],
  },
  {
    title: 'Database',
    icon: Database,
    skills: ['PostgreSQL', 'MySQL', 'SQL Server', 'Redis', 'MongoDB', 'Elasticsearch'],
  },
  {
    title: 'DevOps',
    icon: Cloud,
    skills: ['Docker', 'Kubernetes', 'GitHub Actions', 'AWS', 'Terraform', 'Nginx'],
  },
])

const projects = ref([
  {
    name: 'SmartFlow ERP',
    summary: 'Enterprise resource planning system serving 10k+ daily active users across 5 companies.',
    techs: ['Spring Boot', 'React', 'SQL Server', 'Redis', 'Docker'],
    highlights: [
      'Reduced query latency by 70% via index optimization & N+1 elimination',
      'JWT + RBAC multi-tenant authentication system',
      'Automated month-end closing workflow, saving 40 hrs/month',
    ],
    github: 'https://github.com/sagartia',
    demo: null,
  },
  {
    name: 'DevPulse Monitoring',
    summary: 'Real-time infrastructure monitoring dashboard with intelligent alerting and anomaly detection.',
    techs: ['Go', 'Prometheus', 'Grafana', 'Kubernetes', 'WebSocket'],
    highlights: [
      'Sub-second metric ingestion pipeline handling 500k events/min',
      'ML-based anomaly detection reducing false alerts by 60%',
      'WebSocket live dashboard with 99.9% uptime SLA',
    ],
    github: 'https://github.com/sagartia',
    demo: 'https://github.com/sagartia',
  },
  {
    name: 'QuickCart API',
    summary: 'High-throughput e-commerce API gateway with distributed caching and event-driven order processing.',
    techs: ['Node.js', 'PostgreSQL', 'Redis', 'AWS SQS', 'TypeScript'],
    highlights: [
      'Handles 10k concurrent requests with horizontal auto-scaling',
      'Event-driven order pipeline with guaranteed at-least-once delivery',
      'Idempotent payment processing integrated with Stripe',
    ],
    github: 'https://github.com/sagartia',
    demo: 'https://github.com/sagartia',
  },
  {
    name: 'AuthBridge SDK',
    summary: 'Open-source OAuth 2.0 / OIDC library with support for 12 identity providers.',
    techs: ['TypeScript', 'OAuth 2.0', 'OIDC', 'JWT', 'Node.js'],
    highlights: [
      '2,400+ GitHub stars, used by 300+ projects',
      'Zero-dependency core with tree-shakeable adapters',
      'Comprehensive test suite with 98% code coverage',
    ],
    github: 'https://github.com/sagartia',
    demo: null,
  },
])

const experiences = ref([
  {
    title: 'Senior Full-Stack Engineer',
    company: 'Acme Corp',
    period: '2022 — Present',
    location: 'Taipei, Taiwan',
    summary: 'Leading architecture decisions for a platform serving 500k MAU. Migrated monolith to microservices, cutting deployment frequency from weekly to daily.',
    highlights: [
      'Architected event-driven backend reducing p95 latency from 800ms → 120ms',
      'Mentored a team of 4 engineers, establishing code review and testing standards',
      'Delivered $2M cost reduction by optimizing cloud infrastructure spend',
    ],
  },
  {
    title: 'Full-Stack Engineer',
    company: 'TechWave Solutions',
    period: '2020 — 2022',
    location: 'Remote',
    summary: 'Built and maintained core product features for a B2B SaaS analytics platform. Owned the entire data ingestion pipeline.',
    highlights: [
      'Re-engineered ETL pipeline handling 1TB daily data, 5× throughput improvement',
      'Built React component library adopted across 3 product teams',
      'Integrated Stripe billing, reducing manual ops work by 80%',
    ],
  },
  {
    title: 'Junior Backend Engineer',
    company: 'StartupXYZ',
    period: '2018 — 2020',
    location: 'Taipei, Taiwan',
    summary: 'First engineering hire; built the backend from scratch using Spring Boot and PostgreSQL.',
    highlights: [
      'Designed and implemented REST API powering iOS & Android apps',
      'Set up CI/CD pipeline with GitHub Actions, reducing release time from days to minutes',
      'Achieved 95%+ test coverage on critical payment flows',
    ],
  },
])

const contactLinks = ref([
  { label: 'GitHub', href: 'https://github.com/sagartia', type: 'github' },
  { label: 'LinkedIn', href: 'https://www.linkedin.com/in/shu-yu-yang-44a598417', type: 'linkedin' },
  { label: 'Email', href: 'mailto:sagartiajpjp@gmail.com', type: 'mail' },
])
</script>

<template>
  <div class="bg-gray-950 text-gray-100 antialiased">

    <!-- Header -->
    <header
      class="fixed top-0 inset-x-0 z-50 transition-all duration-300"
      :class="scrolled ? 'bg-gray-950/95 backdrop-blur-sm border-b border-gray-800/50' : 'bg-transparent'"
    >
      <nav class="max-w-6xl mx-auto px-6 h-16 flex items-center justify-between">
        <a href="#hero" class="flex items-center gap-2 font-bold text-emerald-400 tracking-tight text-lg">
          <Terminal :size="20" aria-hidden="true" />
          <span>Shu<span class="text-gray-100">.dev</span></span>
        </a>

        <ul class="hidden md:flex items-center gap-8">
          <li v-for="item in navItems" :key="item.href">
            <a
              :href="item.href"
              class="text-sm text-gray-400 hover:text-emerald-400 transition-colors capitalize"
            >{{ item.label }}</a>
          </li>
          <li>
            <a
              href="#contact"
              class="text-sm px-4 py-2 rounded-lg bg-emerald-500/10 border border-emerald-500/30 text-emerald-400 hover:bg-emerald-500/20 transition-colors"
            >Hire Me</a>
          </li>
        </ul>

        <div class="flex items-center gap-3">
          <!-- Dark / Light toggle -->
          <button
            @click="isDark = !isDark"
            class="relative flex h-6 w-11 items-center rounded-full border border-gray-700 bg-gray-800 transition-colors hover:border-emerald-500/50"
            :aria-label="isDark ? 'Switch to light mode' : 'Switch to dark mode'"
          >
            <span
              class="absolute flex h-5 w-5 items-center justify-center rounded-full bg-gray-600 transition-all duration-300"
              :class="isDark ? 'left-[1px] bg-gray-600' : 'left-[21px] bg-emerald-400'"
            >
              <Moon v-if="isDark" :size="11" class="text-gray-300" />
              <Sun v-else :size="11" class="text-gray-950" />
            </span>
          </button>

          <!-- Mobile menu button -->
          <button class="md:hidden text-gray-400 hover:text-white transition-colors" aria-label="Toggle menu">
            <Menu :size="22" aria-hidden="true" />
          </button>
        </div>
      </nav>
    </header>

    <main>

      <!-- Hero -->
      <section id="hero" class="relative min-h-screen flex flex-col justify-center px-6 pt-16 overflow-hidden">
        <!-- grid background -->
        <div class="absolute inset-0 bg-[linear-gradient(to_right,#1f2937_1px,transparent_1px),linear-gradient(to_bottom,#1f2937_1px,transparent_1px)] bg-[size:4rem_4rem] opacity-20 pointer-events-none"></div>
        <!-- glow -->
        <div class="absolute top-1/3 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[600px] h-[600px] bg-emerald-500/5 rounded-full blur-3xl pointer-events-none"></div>

        <div class="relative max-w-6xl mx-auto w-full">
          <div class="inline-flex items-center gap-2 text-xs text-emerald-400 bg-emerald-500/10 border border-emerald-500/20 px-3 py-1.5 rounded-full mb-6">
            <span class="w-1.5 h-1.5 rounded-full bg-emerald-400 animate-pulse"></span>
            Available for new opportunities
          </div>

          <h1 class="text-5xl md:text-7xl font-black tracking-tight mb-6 leading-none">
            <span class="block text-gray-100">Full-Stack</span>
            <span class="block text-emerald-400">Engineer.</span>
          </h1>

          <p class="text-lg md:text-xl text-gray-400 max-w-2xl mb-8 leading-relaxed">
            Focused on building
            <span class="text-gray-200 font-medium">high-performance, scalable architectures</span>
            that solve real problems. 6+ years turning complex requirements into clean, maintainable systems.
          </p>

          <div class="flex flex-wrap gap-4">
            <a
              href="#projects"
              class="inline-flex items-center gap-2 px-6 py-3 bg-emerald-500 hover:bg-emerald-400 text-gray-950 font-semibold rounded-lg transition-colors"
            >
              View Projects
              <ArrowRight :size="16" aria-hidden="true" />
            </a>
            <a
              href="#contact"
              class="inline-flex items-center gap-2 px-6 py-3 bg-gray-800 hover:bg-gray-700 text-gray-100 font-semibold rounded-lg border border-gray-700 transition-colors"
            >
              Contact Me
            </a>
          </div>

          <div class="flex items-center gap-6 mt-12 text-sm text-gray-500">
            <span class="flex items-center gap-1.5">
              <MapPin :size="14" aria-hidden="true" /> Taipei, Taiwan
            </span>
            <span class="flex items-center gap-1.5">
              <Layers :size="14" aria-hidden="true" /> 6+ yrs experience
            </span>
            <span class="flex items-center gap-1.5">
              <Zap :size="14" aria-hidden="true" /> Open to remote
            </span>
          </div>
        </div>

        <div class="absolute bottom-8 left-1/2 -translate-x-1/2 text-gray-600 animate-bounce">
          <ChevronDown :size="20" aria-hidden="true" />
        </div>
      </section>

      <!-- About & Skills -->
      <section id="about" class="py-24 px-6">
        <div class="max-w-6xl mx-auto">
          <p class="text-xs font-semibold tracking-widest text-emerald-500 uppercase mb-2">About &amp; Skills</p>
          <h2 class="text-3xl md:text-4xl font-bold mb-6 text-gray-100">Who I Am</h2>

          <div class="grid md:grid-cols-2 gap-12 mb-16">
            <p class="text-gray-400 leading-relaxed text-lg">
              I'm a full-stack engineer who cares deeply about
              <span class="text-gray-200">system design, developer experience, and code quality</span>.
              I've built products from zero to scale — from designing database schemas to shipping pixel-perfect UIs.
            </p>
            <p class="text-gray-400 leading-relaxed text-lg">
              My sweet spot is the backend: distributed systems, API design, and performance optimization.
              But I'm equally comfortable in the frontend, shipping
              <span class="text-gray-200">React apps that are fast, accessible, and maintainable</span>.
            </p>
          </div>

          <div class="grid sm:grid-cols-2 lg:grid-cols-4 gap-6">
            <div
              v-for="group in skillGroups"
              :key="group.title"
              class="bg-gray-900 border border-gray-800 rounded-xl p-5 hover:border-emerald-500/30 transition-colors"
            >
              <div class="flex items-center gap-2 text-emerald-400 mb-4 font-semibold text-sm">
                <component :is="group.icon" :size="16" aria-hidden="true" />
                {{ group.title }}
              </div>
              <div class="flex flex-wrap gap-2">
                <span
                  v-for="skill in group.skills"
                  :key="skill"
                  class="text-xs px-2 py-1 bg-gray-800 text-gray-400 rounded-md border border-gray-700"
                >{{ skill }}</span>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- Projects -->
      <section id="projects" class="py-24 px-6 bg-gray-900/30">
        <div class="max-w-6xl mx-auto">
          <p class="text-xs font-semibold tracking-widest text-emerald-500 uppercase mb-2">Side Projects</p>
          <h2 class="text-3xl md:text-4xl font-bold mb-4 text-gray-100">Things I've Built</h2>
          <p class="text-gray-500 mb-12 text-lg">A selection of projects that demonstrate my technical range.</p>

          <div class="grid md:grid-cols-2 gap-6">
            <div
              v-for="project in projects"
              :key="project.name"
              class="group bg-gray-900 border border-gray-800 rounded-xl p-6 hover:border-emerald-500/40 transition-all duration-300"
            >
              <div class="flex items-start justify-between mb-3">
                <h3 class="text-lg font-bold text-gray-100 group-hover:text-emerald-400 transition-colors">
                  {{ project.name }}
                </h3>
                <div class="flex items-center gap-3 ml-4">
                  <a
                    :href="project.github"
                    target="_blank"
                    rel="noopener noreferrer"
                    class="text-gray-500 hover:text-emerald-400 transition-colors"
                    aria-label="GitHub"
                  >
                    <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"/><path d="M9 18c-4.51 2-5-2-7-2"/></svg>
                  </a>
                  <a
                    v-if="project.demo"
                    :href="project.demo"
                    target="_blank"
                    rel="noopener noreferrer"
                    class="text-gray-500 hover:text-emerald-400 transition-colors"
                    aria-label="Live Demo"
                  >
                    <ExternalLink :size="18" aria-hidden="true" />
                  </a>
                </div>
              </div>

              <p class="text-gray-500 text-sm mb-4">{{ project.summary }}</p>

              <div class="flex flex-wrap gap-2 mb-5">
                <span
                  v-for="tech in project.techs"
                  :key="tech"
                  class="text-xs px-2 py-0.5 bg-emerald-500/10 text-emerald-400 border border-emerald-500/20 rounded-md"
                >{{ tech }}</span>
              </div>

              <ul class="space-y-1.5">
                <li
                  v-for="h in project.highlights"
                  :key="h"
                  class="flex items-start gap-2 text-xs text-gray-500"
                >
                  <span class="text-emerald-500 mt-0.5 shrink-0">›</span>
                  {{ h }}
                </li>
              </ul>
            </div>
          </div>
        </div>
      </section>

      <!-- Experience -->
      <section id="experience" class="py-24 px-6">
        <div class="max-w-4xl mx-auto">
          <p class="text-xs font-semibold tracking-widest text-emerald-500 uppercase mb-2">Experience</p>
          <h2 class="text-3xl md:text-4xl font-bold mb-12 text-gray-100">Work History</h2>

          <div class="relative">
            <!-- vertical line -->
            <div class="absolute left-0 top-2 bottom-2 w-px bg-gradient-to-b from-emerald-500 via-emerald-500/30 to-transparent hidden md:block"></div>

            <div class="space-y-12">
              <div
                v-for="item in experiences"
                :key="item.title"
                class="md:pl-10 relative"
              >
                <!-- dot -->
                <div class="absolute left-[-4.5px] top-1.5 w-2.5 h-2.5 rounded-full bg-emerald-500 border-2 border-gray-950 hidden md:block"></div>

                <div class="bg-gray-900 border border-gray-800 rounded-xl p-6 hover:border-emerald-500/30 transition-colors">
                  <div class="flex flex-wrap items-start justify-between gap-3 mb-3">
                    <div>
                      <h3 class="text-lg font-bold text-gray-100">{{ item.title }}</h3>
                      <p class="text-emerald-400 font-medium text-sm">{{ item.company }}</p>
                    </div>
                    <div class="text-right text-xs text-gray-500 space-y-1">
                      <div class="flex items-center gap-1.5 justify-end">
                        <Calendar :size="12" aria-hidden="true" />
                        {{ item.period }}
                      </div>
                      <div class="flex items-center gap-1.5 justify-end">
                        <MapPin :size="12" aria-hidden="true" />
                        {{ item.location }}
                      </div>
                    </div>
                  </div>

                  <p class="text-gray-500 text-sm mb-4 leading-relaxed">{{ item.summary }}</p>

                  <ul class="space-y-1.5">
                    <li
                      v-for="h in item.highlights"
                      :key="h"
                      class="flex items-start gap-2 text-xs text-gray-400"
                    >
                      <span class="text-emerald-500 mt-0.5 shrink-0">✓</span>
                      {{ h }}
                    </li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- Contact -->
      <section id="contact" class="py-24 px-6 bg-gray-900/30">
        <div class="max-w-2xl mx-auto text-center">
          <p class="text-xs font-semibold tracking-widest text-emerald-500 uppercase mb-2">Contact</p>
          <h2 class="text-3xl md:text-4xl font-bold mb-4 text-gray-100">Let's Work Together</h2>
          <p class="text-gray-500 text-lg mb-10">
            I'm open to full-time roles, freelance projects, and interesting collaborations.<br />
            Drop me a message and I'll get back to you within 24 hours.
          </p>

          <a
            href="mailto:sagartiajpjp@gmail.com"
            class="inline-flex items-center gap-3 px-8 py-4 bg-emerald-500 hover:bg-emerald-400 text-gray-950 font-bold rounded-xl text-lg transition-colors mb-12"
          >
            <Mail :size="20" aria-hidden="true" />
            sagartiajpjp@gmail.com
          </a>

          <div class="flex items-center justify-center gap-6">
            <a
              v-for="link in contactLinks"
              :key="link.label"
              :href="link.href"
              target="_blank"
              rel="noopener noreferrer"
              :aria-label="link.label"
              class="flex items-center gap-2 text-gray-500 hover:text-emerald-400 transition-colors text-sm"
            >
              <!-- GitHub -->
              <svg v-if="link.type === 'github'" xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"/><path d="M9 18c-4.51 2-5-2-7-2"/></svg>
              <!-- LinkedIn -->
              <svg v-else-if="link.type === 'linkedin'" xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"/><rect width="4" height="12" x="2" y="9"/><circle cx="4" cy="4" r="2"/></svg>
              <!-- Mail -->
              <Mail v-else :size="22" aria-hidden="true" />
              <span>{{ link.label }}</span>
            </a>
          </div>
        </div>
      </section>

    </main>

    <footer class="py-8 px-6 border-t border-gray-800/60 text-center text-sm text-gray-600">
      <p>Built with Vue 3 &amp; Tailwind CSS · Deployed on Netlify</p>
    </footer>

  </div>
</template>
