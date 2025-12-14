<script setup lang="ts">
import { ref, onMounted } from 'vue'
import SectionTitle from './SectionTitle.vue'
import ProjectCard from './ProjectCard.vue'

const isVisible = ref(false)
const sectionRef = ref<HTMLElement | null>(null)
const activeFilter = ref('all')

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

const filters = [
  { id: 'all', label: 'All Projects' },
  { id: 'ai', label: 'AI/ML' },
  { id: 'medical', label: 'Medical' },
  { id: 'iot', label: 'IoT/Hardware' }
]

const projects = [
  {
    title: 'Uphasia',
    description: 'AI application for Aphasia patients using LLM + ASR technology to assist with speech therapy and communication.',
    tag: 'Startup/AI',
    tagColor: 'purple',
    image: 'https://i.ytimg.com/vi/cvhsDRYagVo/maxresdefault.jpg',
    category: 'ai',
    tech: ['Python', 'Typhoon LLM', 'RAG', 'FastAPI'],
    year: '2023-2025',
    role: 'Co-founder & PM',
    link: 'https://uphasia.co/'
  },
  {
    title: 'Ear Cancer Classification',
    description: 'Medical AI system using ResNet + Vision Transformers for accurate ear cancer detection from medical imaging.',
    tag: 'Medical AI',
    tagColor: 'rose',
    image: '/images/projects/ear-cancer.png',
    category: 'medical',
    tech: ['PyTorch', 'ResNet', 'ViT', 'Python'],
    year: '2024',
    role: 'AI Engineer'
  },
  {
    title: 'TEEOR',
    description: 'AI Builders project - Procurement Checker Tool utilizing OCR + NLP for automated government document verification.',
    tag: 'GovTech',
    tagColor: 'blue',
    image: '/images/projects/teeor.png',
    category: 'ai',
    tech: ['NLP', 'OCR', 'Python', 'NER'],
    year: '2023',
    role: 'AI Developer',
    link: 'https://medium.com/@pataradany/teeor-the-first-procurement-books-checker-tool-of-thailand-8c794987fbba'
  },
  {
    title: 'Brain Stroke Segmentation',
    description: '3D Reconstruction from CT Scans using U-Net architecture for precise brain stroke analysis and treatment planning.',
    tag: 'Medical Imaging',
    tagColor: 'emerald',
    image: '/images/projects/brain-stroke.png',
    category: 'medical',
    tech: ['U-Net', 'PyTorch', '3D Modeling', 'CT Scan'],
    year: '2024',
    role: 'Lead Developer'
  },
  {
    title: 'Satellite Drought Warning',
    description: 'IoT-based satellite system for early drought detection. Winner of GISTDA School Satellite Competition 2024.',
    tag: 'IoT/Space',
    tagColor: 'orange',
    image: '/images/projects/satellite.png',
    category: 'iot',
    tech: ['Raspberry Pi', 'IoT', 'Python', 'Sensors'],
    year: '2024',
    role: 'Tech Lead'
  },
  {
    title: 'Cansat Rocket System',
    description: 'Complete flight software and deployment system for Thailand Cansat-Rocket Competition. Rocket Consolation Award.',
    tag: 'Robotics',
    tagColor: 'cyan',
    image: '/images/projects/cansat.png',
    category: 'iot',
    tech: ['C++', 'Arduino', 'Flight Software', 'Telemetry'],
    year: '2024',
    role: 'Software Engineer'
  }
]

const filteredProjects = ref(projects)

const filterProjects = (category: string) => {
  activeFilter.value = category
  if (category === 'all') {
    filteredProjects.value = projects
  } else {
    filteredProjects.value = projects.filter((p) => p.category === category)
  }
}
</script>

<template>
  <section id="projects" ref="sectionRef" class="py-20">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
      <SectionTitle title="Featured Projects" subtitle="What I've built" />

      <!-- Filter Tabs -->
      <div
        :class="[
          'flex flex-wrap justify-center gap-2 mb-10 transition-all duration-500',
          isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'
        ]"
      >
        <button
          v-for="filter in filters"
          :key="filter.id"
          @click="filterProjects(filter.id)"
          :class="[
            'px-4 py-2 rounded-full text-sm font-medium transition-all duration-300',
            activeFilter === filter.id
              ? 'bg-primary-600 text-white shadow-lg shadow-primary-600/25'
              : 'bg-slate-800/50 text-slate-400 hover:text-white hover:bg-slate-700/50'
          ]"
        >
          {{ filter.label }}
        </button>
      </div>

      <!-- Projects Grid -->
      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
        <ProjectCard
          v-for="(project, index) in filteredProjects"
          :key="project.title"
          v-bind="project"
          :class="[
            'transition-all duration-500',
            isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'
          ]"
          :style="{ transitionDelay: `${index * 100}ms` }"
        />
      </div>

      <!-- View More -->
      <div
        :class="[
          'text-center mt-10 transition-all duration-500',
          isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'
        ]"
        :style="{ transitionDelay: '600ms' }"
      >
        <a
          href="https://github.com/fifaak"
          target="_blank"
          rel="noopener noreferrer"
          class="inline-flex items-center gap-2 px-6 py-3 border border-slate-700 text-slate-300 hover:text-white hover:border-primary-500 rounded-lg transition-all duration-300"
        >
          <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
            <path
              d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"
            />
          </svg>
          View More on GitHub
        </a>
      </div>
    </div>
  </section>
</template>
