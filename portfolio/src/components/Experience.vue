<script setup lang="ts">
import { ref, onMounted } from 'vue'
import SectionTitle from './SectionTitle.vue'

const isVisible = ref(false)
const sectionRef = ref<HTMLElement | null>(null)

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
    logo: 'https://upload.wikimedia.org/wikipedia/commons/thumb/5/5e/Garuda_Emblem_of_Thailand.svg/200px-Garuda_Emblem_of_Thailand.svg.png'
  },
  {
    period: 'Jul 2025 - Sep 2025',
    title: 'AI Researcher & MLOps',
    company: 'Walailak University',
    description: 'Research and development of machine learning solutions for energy optimization.',
    achievement: 'Engineered WattGraphNet achieving 40%+ cost savings',
    type: 'work',
    logo: 'https://upload.wikimedia.org/wikipedia/en/thumb/c/c5/Walailak_University_Logo.svg/200px-Walailak_University_Logo.svg.png'
  },
  {
    period: '2023 - Jan 2025',
    title: 'Project Manager & AI Engineer',
    company: 'Uphasia Co., Ltd.',
    description: 'Co-founded healthtech startup focused on AI-powered solutions for aphasia patients.',
    achievement: 'Developed "Uphasia Workflow" integrating Typhoon 1.5x LLM',
    type: 'work',
    logo: '/images/uphasia-logo.png'
  },
  {
    period: 'Teaching Experience',
    title: 'AI Instructor & Mentor',
    company: 'Mahidol University (AI Builders 5), POSN (KMUTNB), Saraburiwitthayakhom School',
    description: 'Teaching AI/ML fundamentals, mentoring students in project development and competition preparation.',
    achievement: 'Mentored students in AI/ML fundamentals and project development',
    type: 'teaching',
    logo: 'https://upload.wikimedia.org/wikipedia/en/thumb/4/4a/Mahidol_University_%28emblem%29.svg/200px-Mahidol_University_%28emblem%29.svg.png'
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
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
