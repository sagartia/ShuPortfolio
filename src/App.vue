<script setup>
import {
  ArrowUpRight,
  BriefcaseBusiness,
  Code2,
  Database,
  Github,
  Linkedin,
  Mail,
  Rocket,
  Server,
  ShieldCheck,
  Terminal,
} from 'lucide-vue-next'
import { ref } from 'vue'

const navItems = [
  { label: 'About', href: '#about' },
  { label: 'Projects', href: '#projects' },
  { label: 'Experience', href: '#experience' },
  { label: 'Contact', href: '#contact' },
]

const skillGroups = ref([
  {
    title: 'Backend',
    icon: Server,
    skills: ['Java', 'Spring Boot', 'Spring Security', 'RESTful API', 'JWT', 'JPA'],
  },
  {
    title: 'Frontend',
    icon: Code2,
    skills: ['Vue 3', 'HTML', 'CSS', 'JavaScript', 'RWD'],
  },
  {
    title: 'Database',
    icon: Database,
    skills: ['SQL Server', '資料表設計', '查詢優化', '交易控制'],
  },
  {
    title: 'DevOps',
    icon: Terminal,
    skills: ['Git', 'GitHub', 'Postman', 'Docker 基礎', '部署流程'],
  },
])

const projects = ref([
  {
    name: 'E-Commerce Platform',
    summary: '整合會員、購物車、訂單與優惠券流程的全端電商平台。',
    techs: ['Spring Boot', 'Vue 3', 'SQL Server', 'JWT'],
    highlights: ['設計購物車與訂單結帳流程', '實作 JWT 驗證與權限控管', '使用交易控制降低庫存異常風險'],
    github: 'https://github.com/',
    demo: '#',
  },
  {
    name: 'Order Automation System',
    summary: '以排程任務處理訂單狀態轉換，降低人工維護成本。',
    techs: ['Java', 'Spring Scheduler', 'JPA', 'SQL'],
    highlights: ['自動更新送達後訂單狀態', '拆分 service 邏輯提升可維護性', '補強例外情境與資料一致性'],
    github: 'https://github.com/',
    demo: '#',
  },
  {
    name: 'Portfolio Website',
    summary: '以清楚資訊架構展示技能、作品與開發經歷的個人網站。',
    techs: ['Vue 3', 'Tailwind CSS', 'Lucide Icons'],
    highlights: ['建立資料驅動的內容結構', '支援手機與桌面版響應式排版', '以深色視覺呈現科技感品牌形象'],
    github: 'https://github.com/',
    demo: '#',
  },
])

const experiences = ref([
  {
    period: '2026',
    title: 'Java 全端工程師養成班',
    description: '系統學習 Java、Spring Boot、Vue 與資料庫設計，並以電商平台作為期末專案主軸。',
  },
  {
    period: '2026',
    title: '電商平台期末專案開發',
    description: '負責購物車、訂單、優惠券與結帳流程，串接前後端 API 並處理資料一致性。',
  },
  {
    period: '持續中',
    title: 'Side Project 與技術整理',
    description: '透過作品集、API 文件與開發筆記累積可展示的工程能力與問題解決紀錄。',
  },
])

const contactLinks = ref([
  { label: 'GitHub', href: 'https://github.com/sagartia', icon: Github },
  { label: 'LinkedIn', href: 'https://www.linkedin.com/in/shu-yu-yang-44a598417', icon: Linkedin },
  { label: 'Email', href: 'shuyu020515@gmail.com', icon: Mail },
])
</script>

<template>
  <main class="min-h-screen bg-zinc-950 text-zinc-100 selection:bg-emerald-400/30">
    <nav class="sticky top-0 z-50 border-b border-white/10 bg-zinc-950/85 backdrop-blur-xl">
      <div class="mx-auto flex max-w-6xl items-center justify-between px-5 py-4">
        <a href="#" class="flex items-center gap-2 text-sm font-semibold tracking-wide text-white">
          <span class="grid size-9 place-items-center rounded-lg bg-emerald-400 text-zinc-950">
            <Rocket class="size-5" />
          </span>
          SHU Portfolio
        </a>

        <div class="hidden items-center gap-7 text-sm text-zinc-400 md:flex">
          <a
            v-for="item in navItems"
            :key="item.href"
            :href="item.href"
            class="transition hover:text-emerald-300"
          >
            {{ item.label }}
          </a>
        </div>
      </div>
    </nav>

    <section class="mx-auto grid min-h-[calc(100vh-73px)] max-w-6xl items-center gap-12 px-5 py-20 lg:grid-cols-[1.05fr_0.95fr]">
      <div>
        <p class="mb-5 inline-flex items-center gap-2 rounded-full border border-emerald-400/30 bg-emerald-400/10 px-4 py-2 text-sm font-medium text-emerald-300">
          <ShieldCheck class="size-4" />
          Backend / Full-Stack Developer
        </p>
        <h1 class="max-w-4xl text-4xl font-bold leading-tight text-white sm:text-5xl lg:text-6xl">
          專注於高效能、可擴充架構的後端與全端工程師
        </h1>
        <p class="mt-6 max-w-2xl text-base leading-8 text-zinc-400 sm:text-lg">
          我正在累積 Java、Spring Boot、Vue 與資料庫設計的實戰經驗，重視清楚的系統流程、穩定的資料處理，以及能被團隊理解與維護的程式碼。
        </p>
        <div class="mt-9 flex flex-col gap-3 sm:flex-row">
          <a
            href="#projects"
            class="inline-flex items-center justify-center gap-2 rounded-lg bg-emerald-400 px-5 py-3 text-sm font-semibold text-zinc-950 transition hover:bg-emerald-300"
          >
            查看作品
            <ArrowUpRight class="size-4" />
          </a>
          <a
            href="#contact"
            class="inline-flex items-center justify-center gap-2 rounded-lg border border-white/15 px-5 py-3 text-sm font-semibold text-white transition hover:border-emerald-300/70 hover:text-emerald-300"
          >
            聯絡我
            <Mail class="size-4" />
          </a>
        </div>
      </div>

      <div class="relative">
        <div class="absolute -inset-4 rounded-3xl bg-emerald-400/10 blur-3xl"></div>
        <div class="relative rounded-2xl border border-white/10 bg-zinc-900/80 p-6 shadow-2xl shadow-black/30">
          <div class="mb-6 flex items-center justify-between border-b border-white/10 pb-4">
            <div>
              <p class="text-sm text-zinc-500">Current Focus</p>
              <p class="mt-1 font-semibold text-white">E-Commerce Backend Flow</p>
            </div>
            <Terminal class="size-6 text-emerald-300" />
          </div>
          <div class="space-y-4">
            <div class="rounded-lg bg-zinc-950 p-4">
              <p class="text-xs uppercase tracking-widest text-zinc-500">Architecture</p>
              <p class="mt-2 text-sm leading-6 text-zinc-300">Controller -> Service -> Repository -> SQL Server</p>
            </div>
            <div class="grid grid-cols-2 gap-4">
              <div class="rounded-lg border border-white/10 p-4">
                <p class="text-2xl font-bold text-emerald-300">3+</p>
                <p class="mt-1 text-sm text-zinc-400">Side Projects</p>
              </div>
              <div class="rounded-lg border border-white/10 p-4">
                <p class="text-2xl font-bold text-sky-300">10+</p>
                <p class="mt-1 text-sm text-zinc-400">Core Skills</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section id="about" class="border-y border-white/10 bg-zinc-900/40 px-5 py-20">
      <div class="mx-auto max-w-6xl">
        <div class="max-w-3xl">
          <p class="text-sm font-semibold uppercase tracking-widest text-emerald-300">About & Skills</p>
          <h2 class="mt-3 text-3xl font-bold text-white sm:text-4xl">用後端思維打造穩定的全端產品</h2>
          <p class="mt-5 leading-8 text-zinc-400">
            我的學習與專案重點放在電商常見流程：會員驗證、購物車、訂單、優惠券與庫存資料一致性。除了完成畫面與 API 串接，也會思考資料表設計、錯誤處理與未來擴充。
          </p>
        </div>

        <div class="mt-10 grid gap-4 md:grid-cols-2 lg:grid-cols-4">
          <article
            v-for="group in skillGroups"
            :key="group.title"
            class="rounded-xl border border-white/10 bg-zinc-950/70 p-5"
          >
            <div class="mb-5 flex items-center gap-3">
              <span class="grid size-10 place-items-center rounded-lg bg-emerald-400/10 text-emerald-300">
                <component :is="group.icon" class="size-5" />
              </span>
              <h3 class="font-semibold text-white">{{ group.title }}</h3>
            </div>
            <div class="flex flex-wrap gap-2">
              <span
                v-for="skill in group.skills"
                :key="skill"
                class="rounded-md border border-white/10 px-3 py-1.5 text-xs text-zinc-300"
              >
                {{ skill }}
              </span>
            </div>
          </article>
        </div>
      </div>
    </section>

    <section id="projects" class="px-5 py-20">
      <div class="mx-auto max-w-6xl">
        <div class="flex flex-col justify-between gap-6 md:flex-row md:items-end">
          <div>
            <p class="text-sm font-semibold uppercase tracking-widest text-emerald-300">Side Projects</p>
            <h2 class="mt-3 text-3xl font-bold text-white sm:text-4xl">精選作品</h2>
          </div>
          <p class="max-w-xl leading-7 text-zinc-400">
            每個專案都聚焦在真實開發會遇到的問題：資料流程、驗證機制、狀態轉換與可維護性。
          </p>
        </div>

        <div class="mt-10 grid gap-5 lg:grid-cols-3">
          <article
            v-for="project in projects"
            :key="project.name"
            class="flex min-h-[360px] flex-col rounded-xl border border-white/10 bg-zinc-900/70 p-6 transition hover:border-emerald-300/50"
          >
            <div class="flex items-start justify-between gap-4">
              <div>
                <h3 class="text-xl font-bold text-white">{{ project.name }}</h3>
                <p class="mt-3 leading-7 text-zinc-400">{{ project.summary }}</p>
              </div>
              <div class="flex shrink-0 gap-2">
                <a :href="project.github" class="text-zinc-500 transition hover:text-emerald-300" aria-label="GitHub">
                  <Github class="size-5" />
                </a>
                <a :href="project.demo" class="text-zinc-500 transition hover:text-emerald-300" aria-label="Demo">
                  <ArrowUpRight class="size-5" />
                </a>
              </div>
            </div>

            <div class="mt-5 flex flex-wrap gap-2">
              <span
                v-for="tech in project.techs"
                :key="tech"
                class="rounded-md bg-sky-400/10 px-3 py-1 text-xs font-medium text-sky-200"
              >
                {{ tech }}
              </span>
            </div>

            <ul class="mt-6 space-y-3 text-sm leading-6 text-zinc-300">
              <li v-for="highlight in project.highlights" :key="highlight" class="flex gap-3">
                <span class="mt-2 size-1.5 rounded-full bg-emerald-300"></span>
                <span>{{ highlight }}</span>
              </li>
            </ul>
          </article>
        </div>
      </div>
    </section>

    <section id="experience" class="border-y border-white/10 bg-zinc-900/40 px-5 py-20">
      <div class="mx-auto max-w-4xl">
        <p class="text-sm font-semibold uppercase tracking-widest text-emerald-300">Experience</p>
        <h2 class="mt-3 text-3xl font-bold text-white sm:text-4xl">開發經歷與里程碑</h2>

        <div class="mt-10 space-y-8">
          <article v-for="item in experiences" :key="item.title" class="relative grid gap-4 border-l border-white/10 pl-7 sm:grid-cols-[120px_1fr]">
            <span class="absolute -left-[5px] top-2 size-2.5 rounded-full bg-emerald-300"></span>
            <p class="text-sm font-semibold text-emerald-300">{{ item.period }}</p>
            <div>
              <h3 class="font-semibold text-white">{{ item.title }}</h3>
              <p class="mt-2 leading-7 text-zinc-400">{{ item.description }}</p>
            </div>
          </article>
        </div>
      </div>
    </section>

    <section id="contact" class="px-5 py-20">
      <div class="mx-auto max-w-3xl text-center">
        <BriefcaseBusiness class="mx-auto size-10 text-emerald-300" />
        <h2 class="mt-5 text-3xl font-bold text-white sm:text-4xl">期待與你交流</h2>
        <div class="mt-8 flex justify-center gap-3">
          <a
            v-for="link in contactLinks"
            :key="link.label"
            :href="link.href"
            class="grid size-12 place-items-center rounded-lg border border-white/10 text-zinc-400 transition hover:border-emerald-300/60 hover:text-emerald-300"
            :aria-label="link.label"
          >
            <component :is="link.icon" class="size-5" />
          </a>
        </div>
      </div>
    </section>
  </main>
</template>
