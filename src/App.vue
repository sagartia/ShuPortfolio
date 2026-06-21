<script setup>
import {
  ArrowRight,
  Calendar,
  ChevronDown,
  ChevronLeft,
  ChevronRight,
  Code2,
  Database,
  ExternalLink,
  Images,
  Mail,
  MapPin,
  Menu,
  Moon,
  Server,
  Sun,
  Terminal,
  X,
} from 'lucide-vue-next'
import { computed, ref, watch, onMounted, onUnmounted } from 'vue'

const navItems = [
  { label: 'about', href: '#about' },
  { label: 'projects', href: '#projects' },
  { label: 'experience', href: '#experience' },
  // { label: 'contact', href: '#contact' },
]

const scrolled = ref(false)
const onScroll = () => { scrolled.value = window.scrollY > 10 }

const previewProject = ref(null)
const previewIndex = ref(0)
const activePreviewImage = computed(() => previewProject.value?.previewImages?.[previewIndex.value])

const openPreview = (project, index = 0) => {
  previewProject.value = project
  previewIndex.value = index
}

const closePreview = () => {
  previewProject.value = null
  previewIndex.value = 0
}

const showPreviousPreview = () => {
  const total = previewProject.value?.previewImages?.length ?? 0
  if (total) previewIndex.value = (previewIndex.value - 1 + total) % total
}

const showNextPreview = () => {
  const total = previewProject.value?.previewImages?.length ?? 0
  if (total) previewIndex.value = (previewIndex.value + 1) % total
}

const onKeydown = (event) => {
  if (!previewProject.value) return
  if (event.key === 'Escape') closePreview()
  if (event.key === 'ArrowLeft') showPreviousPreview()
  if (event.key === 'ArrowRight') showNextPreview()
}

onMounted(() => {
  window.addEventListener('scroll', onScroll)
  window.addEventListener('keydown', onKeydown)
})

onUnmounted(() => {
  window.removeEventListener('scroll', onScroll)
  window.removeEventListener('keydown', onKeydown)
  document.body.style.overflow = ''
})

watch(previewProject, (project) => {
  document.body.style.overflow = project ? 'hidden' : ''
})

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
    skills: ['Java', 'Spring Boot', 'Spring MVC', 'Spring Security', 'Spring AI', 'Hibernate', 'RESTful API'],
  },
  {
    title: 'Frontend',
    icon: Code2,
    skills: ['HTML', 'CSS', 'JavaScript', 'Vue.js', 'Vite'],
  },
  {
    title: 'Database',
    icon: Database,
    skills: ['SQL Server', 'ChromaDB', '資料表設計', 'JPA / ORM', '交易控制', '資料一致性'],
  },
  {
    title: 'Tools',
    icon: Terminal,
    skills: ['Git', 'GitHub', 'GitHub Models', 'Docker 基礎', 'Linux CLI', 'VS Code'],
  },
])

const projects = ref([
  {
    name: 'C2C 電商購物平台',
    summary: '五人團隊協作開發的全端電商專題，負責從購物車到訂單成立的完整購買流程。',
    techs: ['Spring Boot', 'Spring Security', 'Hibernate', 'SQL Server', 'Vue.js'],
    highlights: [
      '負責購物車、優惠券、結帳與訂單模組，完成跨模組購買流程',
      '設計並實作 15 支 RESTful API，與 Vue 前端完成資料串接',
      '使用 @Transactional 維持結帳、庫存扣減與訂單建立的資料一致性',
      '整合 Spring Security，限制未登入使用者操作購物車與結帳功能',
    ],
    github: 'https://github.com/sagartia',
    demo: null,
    previewImages: [
      {
        src: '/projects/ecommerce-project/ecommerce-1.png',
        alt: '電商平台專案 預覽照'
      },
      {
        src: '/projects/ecommerce-project/ecommerce-2.png',
        alt: '電商平台專案 預覽照'
      },
      {
        src: '/projects/ecommerce-project/ecommerce-3.png',
        alt: '電商平台專案 預覽照'
      },
      {
        src: '/projects/ecommerce-project/ecommerce-4.png',
        alt: '電商平台專案 預覽照'
      },
      {
        src: '/projects/ecommerce-project/ecommerce-5.png',
        alt: '電商平台專案 預覽照'
      },
      {
        src: '/projects/ecommerce-project/ecommerce-6.png',
        alt: '電商平台專案 預覽照'
      },
      {
        src: '/projects/ecommerce-project/ecommerce-7.png',
        alt: '電商平台專案 預覽照'
      },
    ],
  },
  {
    name: 'AI 面試教練｜RAG 專案',
    summary: '依目標職位產生技術面試題，回答後即時取得分數、優缺點與參考答案重點。',
    techs: ['Java 21', 'Spring Boot', 'Spring AI', 'ChromaDB', 'Vue 3', 'GPT-4.1-nano'],
    highlights: [
      '使用 ChromaDB 向量檢索題庫，依職位與題目取得相關內容',
      '透過 Spring AI 串接 GitHub Models 的 GPT-4.1-nano 與 Embedding 模型',
      '實作 0–100 分評分、優缺點分析、參考答案與連續多題流程',
      '以 Vue 3 製作面試對話介面，支援 Ctrl + Enter 快速送出回答',
    ],
    github: 'https://github.com/sagartia/interview-coach',
    demo: null,
    previewImages: [
      {
        src: '/projects/ai-interview-coach/interview-question-and-score.png',
        alt: 'AI 面試教練顯示 Java 面試題、使用者回答與即時評分',
      },
      {
        src: '/projects/ai-interview-coach/interview-feedback-and-next-question.png',
        alt: 'AI 面試教練顯示回答缺點、參考答案重點與下一題',
      },
    ],
  },
  {
    name: '個人履歷與作品集網站',
    summary: '以 Vue 3 建立的響應式個人網站，用來整理技術能力、專題成果與轉職經歷。',
    techs: ['Vue 3', 'JavaScript', 'Tailwind CSS', 'Vite', 'Cloudflare Pages'],
    highlights: [
      '使用 Composition API 與資料陣列管理技能、專案和經歷內容',
      '完成手機與桌面版響應式排版，並支援深色與淺色模式',
      '串接 GitHub 自動部署至 Cloudflare Pages，持續更新個人作品內容',
    ],
    github: 'https://github.com/sagartia/ShuPortfolio',
    demo: 'https://shuportfolio.pages.dev/',
  },
])

const experiences = ref([
  {
    title: '跨域 Java 軟體工程師就業養成班',
    company: '資展國際｜EEIT218',
    period: '2026｜4 個月',
    location: 'Taipei, Taiwan',
    summary: '完成約 450 小時的 Java 全端訓練，學習 Java、Spring、Hibernate、SQL Server、Vue.js、Git 與 Docker。',
    highlights: [
      '在五人團隊中負責電商平台的購物車、優惠券、結帳與訂單模組',
      '參與 API 規格確認、Git 分支整合、跨模組測試與問題排查',
      '透過專題實作理解交易控制、權限驗證與前後端協作流程',
    ],
  },
  {
    title: '資料檢核專員（約僱）',
    company: '國家圖書館',
    period: '2024.05 — 2026.02',
    location: 'Taipei, Taiwan',
    summary: '先後任職於國際標準書號中心與圖書館事業發展組，負責大量書目資料的審核、校正與品質控管。',
    highlights: [
      '平均每月審核與編配約 800 件電子書 ISBN 申請案件',
      '每月檢核約 600 套、4,000 筆公共圖書館套書資料',
      '累積嚴謹的資料處理、文件撰寫、跨單位協作與問題追蹤能力',
    ],
  },
  {
    title: '中國文學系 學士',
    company: '國立中央大學',
    period: '2019.09 — 2023.06',
    location: 'Taoyuan, Taiwan',
    summary: '中文系訓練培養了文字表達、資訊整理與細節敏感度，轉入程式開發後持續運用在需求拆解與團隊溝通。',
    highlights: [
      '能將龐雜資訊整理成清楚結構，協助釐清需求與問題範圍',
      'TOEIC 845 分，具備英文技術文件閱讀基礎',
      '課外持續學習 CS50、資料結構與演算法及 Linux 基礎操作',
    ],
  },
])

const contactLinks = ref([
  { label: 'GitHub', href: 'https://github.com/sagartia', type: 'github' },
  // { label: 'LinkedIn', href: 'https://www.linkedin.com/in/shu-yu-yang-44a598417', type: 'linkedin' },
  { label: 'Email', href: 'mailto:shuyu020515@gmail.com', type: 'mail' },
])
</script>

<template>
  <div class="bg-white text-gray-900 antialiased dark:bg-gray-950 dark:text-gray-100 transition-colors duration-300">

    <!-- Header -->
    <header
      class="fixed top-0 inset-x-0 z-50 transition-all duration-300"
      :class="scrolled
        ? 'bg-white/95 dark:bg-gray-950/95 backdrop-blur-sm border-b border-gray-200 dark:border-gray-800/50'
        : 'bg-transparent'"
    >
      <nav class="max-w-6xl mx-auto px-6 h-16 flex items-center justify-between">
        <a href="#hero" class="flex items-center gap-2 font-bold text-emerald-500 dark:text-emerald-400 tracking-tight text-lg">
          <Terminal :size="20" aria-hidden="true" />
          <span>Shu<span class="text-gray-900 dark:text-gray-100">.dev</span></span>
        </a>

        <ul class="hidden md:flex items-center gap-8">
          <li v-for="item in navItems" :key="item.href">
            <a
              :href="item.href"
              class="text-sm text-gray-500 hover:text-emerald-500 dark:text-gray-400 dark:hover:text-emerald-400 transition-colors capitalize"
            >{{ item.label }}</a>
          </li>
          <li>
            <a
              href="#contact"
              class="text-sm px-4 py-2 rounded-lg bg-emerald-500/10 border border-emerald-500/30 text-emerald-600 dark:text-emerald-400 hover:bg-emerald-500/20 transition-colors"
            >Contact Me</a>
          </li>
        </ul>

        <div class="flex items-center gap-3">
          <!-- Dark / Light toggle -->
          <button
            @click="isDark = !isDark"
            class="relative flex h-6 w-11 items-center rounded-full border transition-colors duration-300"
            :class="isDark
              ? 'bg-gray-700 border-gray-600 hover:border-emerald-500/50'
              : 'bg-gray-200 border-gray-300 hover:border-emerald-500/50'"
            :aria-label="isDark ? 'Switch to light mode' : 'Switch to dark mode'"
          >
            <span
              class="absolute flex h-5 w-5 items-center justify-center rounded-full transition-all duration-300"
              :class="isDark
                ? 'left-[1px] bg-gray-500'
                : 'left-[21px] bg-emerald-400'"
            >
              <Moon v-if="isDark" :size="11" class="text-gray-200" />
              <Sun v-else :size="11" class="text-white" />
            </span>
          </button>

          <!-- Mobile menu button -->
          <button
            class="md:hidden text-gray-500 hover:text-gray-900 dark:text-gray-400 dark:hover:text-white transition-colors"
            aria-label="Toggle menu"
          >
            <Menu :size="22" aria-hidden="true" />
          </button>
        </div>
      </nav>
    </header>

    <main>

      <!-- Hero -->
      <section id="hero" class="relative min-h-screen flex flex-col justify-center px-6 pt-16 overflow-hidden">
        <!-- grid background -->
        <div class="absolute inset-0 bg-[linear-gradient(to_right,#e5e7eb_1px,transparent_1px),linear-gradient(to_bottom,#e5e7eb_1px,transparent_1px)] dark:bg-[linear-gradient(to_right,#1f2937_1px,transparent_1px),linear-gradient(to_bottom,#1f2937_1px,transparent_1px)] bg-[size:4rem_4rem] opacity-60 dark:opacity-20 pointer-events-none"></div>
        <!-- glow -->
        <div class="absolute top-1/3 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[600px] h-[600px] bg-emerald-500/5 rounded-full blur-3xl pointer-events-none"></div>

        <div class="relative max-w-6xl mx-auto w-full">
          <div class="inline-flex items-center gap-2 text-xs text-emerald-600 dark:text-emerald-400 bg-emerald-500/10 border border-emerald-500/20 px-3 py-1.5 rounded-full mb-6">
            <span class="w-1.5 h-1.5 rounded-full bg-emerald-400 animate-pulse"></span>
            Seeking junior Java backend opportunities
          </div>

          <h1 class="text-5xl md:text-7xl font-black tracking-tight mb-6 leading-none">
            <span class="block text-gray-900 dark:text-gray-100">Java Backend</span>
            <span class="block text-emerald-500 dark:text-emerald-400">Developer.</span>
          </h1>

          <p class="text-lg md:text-xl text-gray-500 dark:text-gray-400 max-w-2xl mb-8 leading-relaxed">
            文組轉職的 Java 後端工程師，具備
            <span class="text-gray-800 dark:text-gray-200 font-medium">450 小時全端培訓與 C2C 電商平台實作經驗</span>，
            重視需求拆解、資料正確性與可維護的程式碼。
          </p>

          <div class="flex flex-wrap gap-4">
            <a
              href="#projects"
              class="inline-flex items-center gap-2 px-6 py-3 bg-emerald-500 hover:bg-emerald-400 text-white font-semibold rounded-lg transition-colors"
            >
              View Projects
              <ArrowRight :size="16" aria-hidden="true" />
            </a>
            <!-- <a
              href="#contact"
              class="inline-flex items-center gap-2 px-6 py-3 bg-gray-100 hover:bg-gray-200 dark:bg-gray-800 dark:hover:bg-gray-700 text-gray-800 dark:text-gray-100 font-semibold rounded-lg border border-gray-200 dark:border-gray-700 transition-colors"
            >
              Contact Me
            </a> -->
          </div>

          <div class="flex items-center gap-6 mt-12 text-sm text-gray-400 dark:text-gray-500">
            <span class="flex items-center gap-1.5">
              <MapPin :size="14" aria-hidden="true" /> Taipei, Taiwan
            </span>
            <!-- <span class="flex items-center gap-1.5">
              <Zap :size="14" aria-hidden="true" /> TOEIC 845
            </span> -->
          </div>
        </div>

        <div class="absolute bottom-8 left-1/2 -translate-x-1/2 text-gray-300 dark:text-gray-600 animate-bounce">
          <ChevronDown :size="20" aria-hidden="true" />
        </div>
      </section>

      <!-- About & Skills -->
      <section id="about" class="py-24 px-6">
        <div class="max-w-6xl mx-auto">
          <p class="text-xs font-semibold tracking-widest text-emerald-600 dark:text-emerald-500 uppercase mb-2">About &amp; Skills</p>
          <h2 class="text-3xl md:text-4xl font-bold mb-6 text-gray-900 dark:text-gray-100">從資料檢核走向軟體開發</h2>

          <div class="grid md:grid-cols-2 gap-12 mb-16">
            <p class="text-gray-500 dark:text-gray-400 leading-relaxed text-lg">
              曾經做行政的經驗，面對大量資料審核工作讓我開始思考，
              如何透過程式將規則明確、重複性高的流程做得更有效率，也成為我轉向軟體開發的起點。
            </p>
            <p class="text-gray-500 dark:text-gray-400 leading-relaxed text-lg">
              完成資展國際約 450 小時的 Java 全端培訓後，我在五人電商專題中負責購物車、優惠券、結帳與訂單流程。
              現階段專注於
              <span class="text-gray-800 dark:text-gray-200">Java、Spring Boot、RESTful API 與 SQL Server</span>，
              並持續補強資料結構、演算法與 Linux 基礎。
            </p>
          </div>

          <div class="grid sm:grid-cols-2 lg:grid-cols-4 gap-6">
            <div
              v-for="group in skillGroups"
              :key="group.title"
              class="bg-gray-50 border border-gray-200 dark:bg-gray-900 dark:border-gray-800 rounded-xl p-5 hover:border-emerald-500/30 transition-colors"
            >
              <div class="flex items-center gap-2 text-emerald-600 dark:text-emerald-400 mb-4 font-semibold text-sm">
                <component :is="group.icon" :size="16" aria-hidden="true" />
                {{ group.title }}
              </div>
              <div class="flex flex-wrap gap-2">
                <span
                  v-for="skill in group.skills"
                  :key="skill"
                  class="text-xs px-2 py-1 bg-white border border-gray-200 text-gray-600 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 rounded-md"
                >{{ skill }}</span>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- Projects -->
      <section id="projects" class="py-24 px-6 bg-gray-50 dark:bg-gray-900/30">
        <div class="max-w-6xl mx-auto">
          <p class="text-xs font-semibold tracking-widest text-emerald-600 dark:text-emerald-500 uppercase mb-2">Side Projects</p>
          <h2 class="text-3xl md:text-4xl font-bold mb-4 text-gray-900 dark:text-gray-100">實作專案</h2>
          <p class="text-gray-400 dark:text-gray-500 mb-12 text-lg">以實際開發成果呈現後端流程設計、前後端串接與持續學習紀錄。</p>

          <div class="grid md:grid-cols-2 gap-6">
            <div
              v-for="project in projects"
              :key="project.name"
              class="group bg-white border border-gray-200 dark:bg-gray-900 dark:border-gray-800 rounded-xl p-6 hover:border-emerald-500/40 transition-all duration-300"
            >
              <div class="flex items-start justify-between mb-3">
                <h3 class="text-lg font-bold text-gray-900 dark:text-gray-100 group-hover:text-emerald-500 dark:group-hover:text-emerald-400 transition-colors">
                  {{ project.name }}
                </h3>
                <div class="flex items-center gap-3 ml-4">
                  <a
                    :href="project.github"
                    target="_blank"
                    rel="noopener noreferrer"
                    class="text-gray-400 hover:text-emerald-500 dark:text-gray-500 dark:hover:text-emerald-400 transition-colors"
                    aria-label="GitHub"
                  >
                    <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"/><path d="M9 18c-4.51 2-5-2-7-2"/></svg>
                  </a>
                  <a
                    v-if="project.demo"
                    :href="project.demo"
                    target="_blank"
                    rel="noopener noreferrer"
                    class="text-gray-400 hover:text-emerald-500 dark:text-gray-500 dark:hover:text-emerald-400 transition-colors"
                    aria-label="Live Demo"
                  >
                    <ExternalLink :size="18" aria-hidden="true" />
                  </a>
                </div>
              </div>

              <button
                v-if="project.previewImages?.length"
                type="button"
                class="group/preview relative mb-5 block aspect-video w-full overflow-hidden rounded-lg border border-gray-200 bg-gray-950 text-left dark:border-gray-800"
                :aria-label="`查看 ${project.name} 的成果預覽`"
                @click="openPreview(project)"
              >
                <img
                  :src="project.previewImages[0].src"
                  :alt="project.previewImages[0].alt"
                  class="h-full w-full object-cover object-top transition-transform duration-300 group-hover/preview:scale-[1.02]"
                />
                <span class="absolute inset-x-0 bottom-0 flex items-center justify-between bg-gray-950/85 px-4 py-3 text-sm text-white backdrop-blur-sm">
                  <span class="flex items-center gap-2 font-medium">
                    <Images :size="16" aria-hidden="true" />
                    查看成果預覽
                  </span>
                  <span class="text-xs text-gray-300">{{ project.previewImages.length }} 張</span>
                </span>
              </button>

              <p class="text-gray-500 dark:text-gray-500 text-sm mb-4">{{ project.summary }}</p>

              <div class="flex flex-wrap gap-2 mb-5">
                <span
                  v-for="tech in project.techs"
                  :key="tech"
                  class="text-xs px-2 py-0.5 bg-emerald-500/10 text-emerald-600 dark:text-emerald-400 border border-emerald-500/20 rounded-md"
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
          <p class="text-xs font-semibold tracking-widest text-emerald-600 dark:text-emerald-500 uppercase mb-2">Experience</p>
          <h2 class="text-3xl md:text-4xl font-bold mb-12 text-gray-900 dark:text-gray-100">經歷與學習歷程</h2>

          <div class="relative">
            <div class="absolute left-0 top-2 bottom-2 w-px bg-gradient-to-b from-emerald-500 via-emerald-500/30 to-transparent hidden md:block"></div>

            <div class="space-y-12">
              <div
                v-for="item in experiences"
                :key="item.title"
                class="md:pl-10 relative"
              >
                <div class="absolute left-[-4.5px] top-1.5 w-2.5 h-2.5 rounded-full bg-emerald-500 border-2 border-white dark:border-gray-950 hidden md:block"></div>

                <div class="bg-white border border-gray-200 dark:bg-gray-900 dark:border-gray-800 rounded-xl p-6 hover:border-emerald-500/30 transition-colors">
                  <div class="flex flex-wrap items-start justify-between gap-3 mb-3">
                    <div>
                      <h3 class="text-lg font-bold text-gray-900 dark:text-gray-100">{{ item.title }}</h3>
                      <p class="text-emerald-600 dark:text-emerald-400 font-medium text-sm">{{ item.company }}</p>
                    </div>
                    <div class="text-right text-xs text-gray-400 dark:text-gray-500 space-y-1">
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
                      class="flex items-start gap-2 text-xs text-gray-500 dark:text-gray-400"
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
      <section id="contact" class="py-24 px-6 bg-gray-50 dark:bg-gray-900/30">
        <div class="max-w-2xl mx-auto text-center">
          <p class="text-xs font-semibold tracking-widest text-emerald-600 dark:text-emerald-500 uppercase mb-2">Contact</p>
          <!-- <h2 class="text-3xl md:text-4xl font-bold mb-4 text-gray-900 dark:text-gray-100">期待與你交流</h2> -->
          <p class="text-gray-500 text-lg mb-10">
            目前尋找 Junior Java 後端或全端工程師職缺。<br />
            如果你想進一步了解我的專題與學習經歷，歡迎透過 Email 或 GitHub 與我聯絡。
          </p>

          <a
            href="mailto:shuyu020515@gmail.com"
            class="inline-flex items-center gap-3 px-8 py-4 bg-emerald-500 hover:bg-emerald-400 text-white font-bold rounded-xl text-lg transition-colors mb-12"
          >
            <Mail :size="20" aria-hidden="true" />
          </a>

          <div class="flex items-center justify-center gap-6">
            <a
              v-for="link in contactLinks"
              :key="link.label"
              :href="link.href"
              target="_blank"
              rel="noopener noreferrer"
              :aria-label="link.label"
              class="flex items-center gap-2 text-gray-400 hover:text-emerald-500 dark:text-gray-500 dark:hover:text-emerald-400 transition-colors text-sm"
            >
              <svg v-if="link.type === 'github'" xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"/><path d="M9 18c-4.51 2-5-2-7-2"/></svg>
              <!-- <svg v-else-if="link.type === 'linkedin'" xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"/><rect width="4" height="12" x="2" y="9"/><circle cx="4" cy="4" r="2"/></svg> -->
              <Mail v-else :size="22" aria-hidden="true" />
              <span>{{ link.label }}</span>
            </a>
          </div>
        </div>
      </section>

    </main>

    <footer class="py-8 px-6 border-t border-gray-200 dark:border-gray-800/60 text-center text-sm text-gray-400 dark:text-gray-600">
      <p>Built with Vue 3 &amp; Tailwind CSS · Deployed on Cloudflare Pages</p>
    </footer>

    <Teleport to="body">
      <div
        v-if="previewProject && activePreviewImage"
        class="fixed inset-0 z-[100] flex flex-col bg-gray-950/95 p-4 backdrop-blur-sm sm:p-6"
        role="dialog"
        aria-modal="true"
        :aria-label="`${previewProject.name} 成果預覽`"
        @click.self="closePreview"
      >
        <div class="mx-auto flex w-full max-w-6xl items-center justify-between gap-4 pb-4 text-white">
          <div class="min-w-0">
            <p class="truncate font-semibold">{{ previewProject.name }}</p>
            <p class="mt-1 text-xs text-gray-400">
              {{ previewIndex + 1 }} / {{ previewProject.previewImages.length }}
            </p>
          </div>
          <button
            type="button"
            class="grid size-10 shrink-0 place-items-center rounded-lg border border-white/15 text-gray-300 transition-colors hover:border-emerald-400 hover:text-white"
            aria-label="關閉成果預覽"
            title="關閉"
            @click="closePreview"
          >
            <X :size="20" aria-hidden="true" />
          </button>
        </div>

        <div class="relative mx-auto flex min-h-0 w-full max-w-6xl flex-1 items-center justify-center">
          <button
            v-if="previewProject.previewImages.length > 1"
            type="button"
            class="absolute left-0 z-10 grid size-10 place-items-center rounded-lg border border-white/15 bg-gray-950/80 text-white transition-colors hover:border-emerald-400 sm:left-3"
            aria-label="上一張成果圖"
            title="上一張"
            @click="showPreviousPreview"
          >
            <ChevronLeft :size="22" aria-hidden="true" />
          </button>

          <img
            :src="activePreviewImage.src"
            :alt="activePreviewImage.alt"
            class="max-h-full max-w-full rounded-lg object-contain shadow-2xl shadow-black/50"
          />

          <button
            v-if="previewProject.previewImages.length > 1"
            type="button"
            class="absolute right-0 z-10 grid size-10 place-items-center rounded-lg border border-white/15 bg-gray-950/80 text-white transition-colors hover:border-emerald-400 sm:right-3"
            aria-label="下一張成果圖"
            title="下一張"
            @click="showNextPreview"
          >
            <ChevronRight :size="22" aria-hidden="true" />
          </button>
        </div>

        <div class="mx-auto flex w-full max-w-6xl justify-center gap-3 pt-4">
          <button
            v-for="(image, index) in previewProject.previewImages"
            :key="image.src"
            type="button"
            class="h-14 w-14 overflow-hidden rounded-lg border-2 bg-gray-900 transition-colors sm:h-16 sm:w-16"
            :class="index === previewIndex ? 'border-emerald-400' : 'border-transparent hover:border-white/40'"
            :aria-label="`查看第 ${index + 1} 張成果圖`"
            @click="previewIndex = index"
          >
            <img :src="image.src" :alt="image.alt" class="h-full w-full object-cover object-top" />
          </button>
        </div>
      </div>
    </Teleport>

  </div>
</template>
