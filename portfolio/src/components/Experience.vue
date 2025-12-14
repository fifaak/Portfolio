<script setup lang="ts">
import { ref, onMounted } from 'vue'
import SectionTitle from './SectionTitle.vue'

const isVisible = ref(false)
const sectionRef = ref<HTMLElement | null>(null)
const expandedIndex = ref<number | null>(null)

const toggleExpand = (index: number) => {
  expandedIndex.value = expandedIndex.value === index ? null : index
}

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      if (entries[0]?.isIntersecting) {
        isVisible.value = true
        observer.disconnect()
      }
    },
    { threshold: 0.1 }
  )
  if (sectionRef.value) observer.observe(sectionRef.value)
})

const experiences = [
  {
    period: 'Oct 2025 - Present',
    title: 'Project Manager & Tech Lead',
    company: 'PMUC - Thailand Government',
    description: 'Leading government technology initiatives and digital transformation projects.',
    achievement: 'Reduced workload by automating document review with AI',
    type: 'work',
    logo: 'https://pmuc.or.th/wp-content/uploads/2025/12/pmuc-th-logo.png',
    details: [
      'Led cross-functional team of 5+ members for AI document automation',
      'Implemented RAG-based system for procurement document review',
      'Reduced manual review time by 70% through automation',
      'Collaborated with stakeholders to define project requirements'
    ]
  },
  {
    period: 'Jul 2025 - Sep 2025',
    title: 'AI Researcher & MLOps',
    company: 'Walailak University',
    description: 'Research and development of machine learning solutions for energy optimization.',
    achievement: 'Engineered WattGraphNet achieving 40%+ cost savings',
    type: 'work',
    logo: 'https://i0.wp.com/engineer.wu.ac.th/wp-content/uploads/2020/07/03-standard-abbreviation.png?fit=819%2C577&ssl=1',
    details: [
      'Developed WattGraphNet using Graph Neural Networks for energy prediction',
      'Achieved 40%+ cost savings through optimized energy management',
      'Built MLOps pipeline for model training and deployment',
      'Published research findings and presented to faculty'
    ]
  },
  {
    period: '2023 - Jan 2025',
    title: 'Project Manager & AI Engineer',
    company: 'Uphasia Co., Ltd.',
    description: 'Co-founded healthtech startup focused on AI-powered solutions for aphasia patients.',
    achievement: 'Developed "Uphasia Workflow" integrating Typhoon 1.5x LLM',
    type: 'work',
    logo: 'https://media.licdn.com/dms/image/v2/D4E0BAQEZuhJGLnStHA/company-logo_200_200/company-logo_200_200/0/1710917170075?e=2147483647&v=beta&t=FH0vKI4Alf14edphP2suSZ5qnqTPT5ztPUxfUa40xWk',
    details: [
      'Co-founded startup and led product development from ideation to launch',
      'Integrated Typhoon 1.5x LLM with RAG for personalized therapy',
      'Secured 850,000 THB funding through TechBite 5.0',
      'Won multiple awards including Siriraj Hackathon 2nd Runner-up',
      'Featured on TNN news for innovative healthcare solution'
    ]
  },
  {
    period: 'Teaching Experience',
    title: 'AI Instructor & Mentor',
    company: 'Mahidol University (AI Builders 5), POSN (KMUTNB), Saraburiwitthayakhom School',
    description: 'Teaching AI/ML fundamentals, mentoring students in project development and competition preparation.',
    achievement: 'Mentored students in AI/ML fundamentals and project development',
    type: 'teaching',
    logo: 'https://avatars.githubusercontent.com/u/99741955?s=200&v=4',
    details: [
      'Taught AI/ML fundamentals to 50+ students at AI Builders 5',
      'Mentored POSN students at KMUTNB for programming competitions',
      'Conducted workshops on Python, PyTorch, and NLP',
      'Guided students through end-to-end ML project development'
    ]
  }
]
</script>

<template>
  <section id="experience" ref="sectionRef" class="py-20 bg-slate-900/50">
    <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
      <SectionTitle title="Work Experience" subtitle="My journey" />

      <div class="relative">
        <!-- Timeline line -->
        <div
          class="absolute left-4 md:left-1/2 top-0 bottom-0 w-0.5 bg-gradient-to-b from-primary-500 via-purple-500 to-primary-500/20"
        ></div>

        <div class="space-y-12">
          <div
            v-for="(exp, index) in experiences"
            :key="exp.title"
            :class="[
              'relative transition-all duration-500',
              isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10',
              index % 2 === 0 ? 'md:pr-1/2' : 'md:pl-1/2 md:ml-auto'
            ]"
            :style="{ transitionDelay: `${index * 150}ms` }"
          >
            <!-- Timeline dot -->
            <div
              :class="[
                'absolute left-4 md:left-1/2 w-4 h-4 rounded-full border-4 -translate-x-1/2',
                exp.type === 'teaching'
                  ? 'bg-emerald-500 border-emerald-400'
                  : 'bg-primary-500 border-primary-400'
              ]"
            ></div>

            <!-- Content card -->
            <div
              :class="[
                'ml-12 md:ml-0 p-6 bg-slate-800/50 rounded-xl border border-slate-700/50 hover:border-primary-500/30 transition-all duration-300',
                index % 2 === 0 ? 'md:mr-8' : 'md:ml-8'
              ]"
            >
              <div class="flex items-start gap-4">
                <!-- Company Logo -->
                <div
                  class="w-12 h-12 rounded-lg bg-white/10 flex items-center justify-center flex-shrink-0 overflow-hidden"
                >
                  <img
                    :src="exp.logo"
                    :alt="exp.company"
                    class="w-10 h-10 object-contain"
                    @error="($event.target as HTMLImageElement).style.display = 'none'"
                  />
                </div>
                <div class="flex-1">
                  <span class="text-primary-400 text-sm font-medium">{{ exp.period }}</span>
                  <h3 class="text-xl font-bold text-white mt-1">{{ exp.title }}</h3>
                  <p class="text-slate-400 text-sm mt-1">{{ exp.company }}</p>
                </div>
              </div>
              <p class="text-slate-300 mt-4">{{ exp.description }}</p>
              <div class="mt-4 flex items-start gap-2">
                <span class="text-emerald-400">✓</span>
                <span class="text-slate-400 text-sm">{{ exp.achievement }}</span>
              </div>

              <!-- Expand Button -->
              <button
                @click="toggleExpand(index)"
                class="mt-4 flex items-center gap-2 text-sm text-primary-400 hover:text-primary-300 transition-colors"
              >
                <span>{{ expandedIndex === index ? 'Show less' : 'Show more' }}</span>
                <svg
                  :class="['w-4 h-4 transition-transform duration-300', expandedIndex === index ? 'rotate-180' : '']"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                </svg>
              </button>

              <!-- Expandable Details -->
              <div
                :class="[
                  'overflow-hidden transition-all duration-300',
                  expandedIndex === index ? 'max-h-96 opacity-100 mt-4' : 'max-h-0 opacity-0'
                ]"
              >
                <ul class="space-y-2 pl-4 border-l-2 border-primary-500/30">
                  <li
                    v-for="(detail, detailIndex) in exp.details"
                    :key="detailIndex"
                    class="text-slate-400 text-sm"
                  >
                    {{ detail }}
                  </li>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
