<script setup lang="ts">
import { ref, onMounted } from 'vue'
import SectionTitle from './SectionTitle.vue'
import SkillBadge from './SkillBadge.vue'

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

const skillCategories = [
  {
    name: 'Soft Skills',
    color: 'emerald',
    skills: ['Agile & Scrum', 'Strategic Planning', 'Team Leadership', 'Stakeholder Management', 'Public Speaking']
  },
  {
    name: 'Data Science',
    color: 'blue',
    skills: ['scikit-learn', 'pandas', 'numpy', 'Power BI', 'Plotly']
  },
  {
    name: 'AI/ML',
    color: 'purple',
    skills: ['PyTorch', 'Hugging Face', 'Transformers', 'LLM Integration (RAG)', 'CUDA']
  },
  {
    name: 'Development',
    color: 'orange',
    skills: ['Vue.js', 'Node.js', 'FastAPI', 'MongoDB', 'Docker', 'Git']
  },
  {
    name: 'Cloud',
    color: 'cyan',
    skills: ['AWS', 'GCP', 'Vast AI']
  }
]
</script>

<template>
  <section id="skills" ref="sectionRef" class="py-20">
    <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8">
      <SectionTitle title="Skills & Expertise" subtitle="What I do" />
      
      <div class="space-y-8">
        <div
          v-for="(category, catIndex) in skillCategories"
          :key="category.name"
          :class="[
            'transition-all duration-500',
            isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'
          ]"
          :style="{ transitionDelay: `${catIndex * 100}ms` }"
        >
          <h3 class="text-lg font-semibold text-slate-300 mb-3">{{ category.name }}</h3>
          <div class="flex flex-wrap gap-2">
            <SkillBadge
              v-for="skill in category.skills"
              :key="skill"
              :name="skill"
              :color="category.color"
            />
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
