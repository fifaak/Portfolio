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

const skills = [
  { name: 'Python', color: 'purple' },
  { name: 'PyTorch', color: 'purple' },
  { name: 'Hugging Face', color: 'purple' },
  { name: 'LLM/RAG', color: 'purple' },
  { name: 'Transformers', color: 'purple' },
  { name: 'Vue.js', color: 'emerald' },
  { name: 'FastAPI', color: 'emerald' },
  { name: 'Node.js', color: 'emerald' },
  { name: 'Docker', color: 'blue' },
  { name: 'Git', color: 'blue' },
  { name: 'AWS', color: 'orange' },
  { name: 'GCP', color: 'orange' },
  { name: 'MongoDB', color: 'blue' },
  { name: 'Power BI', color: 'blue' },
  { name: 'Agile/Scrum', color: 'cyan' },
  { name: 'Team Leadership', color: 'cyan' },
  { name: 'Public Speaking', color: 'cyan' }
]

const colorClasses: Record<string, string> = {
  purple: 'bg-purple-500/10 text-purple-400 border-purple-500/30 hover:border-purple-400',
  emerald: 'bg-emerald-500/10 text-emerald-400 border-emerald-500/30 hover:border-emerald-400',
  blue: 'bg-blue-500/10 text-blue-400 border-blue-500/30 hover:border-blue-400',
  orange: 'bg-orange-500/10 text-orange-400 border-orange-500/30 hover:border-orange-400',
  cyan: 'bg-cyan-500/10 text-cyan-400 border-cyan-500/30 hover:border-cyan-400'
}
</script>

<template>
  <section id="skills" ref="sectionRef" class="py-16 bg-slate-900/30">
    <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
      <SectionTitle title="Skills & Expertise" subtitle="What I do" />

      <div
        :class="[
          'flex flex-wrap justify-center gap-3 transition-all duration-500',
          isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'
        ]"
      >
        <span
          v-for="skill in skills"
          :key="skill.name"
          :class="[
            'px-4 py-2 rounded-full text-sm border transition-all duration-300',
            colorClasses[skill.color]
          ]"
        >
          {{ skill.name }}
        </span>
      </div>
    </div>
  </section>
</template>
