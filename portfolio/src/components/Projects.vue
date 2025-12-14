<script setup lang="ts">
import { ref, onMounted } from 'vue'
import SectionTitle from './SectionTitle.vue'
import ProjectCard from './ProjectCard.vue'

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

const projects = [
  {
    title: 'Uphasia',
    description: 'AI application for Aphasia patients using LLM + ASR technology to assist with speech therapy and communication. Integrates Typhoon 1.5x LLM with RAG.',
    tag: 'Startup/AI',
    tagColor: 'purple',
    image: '/images/uphasia.png'
  },
  {
    title: 'Ear Cancer Classification',
    description: 'Medical AI system using ResNet + Vision Transformers for accurate ear cancer detection and classification from medical imaging.',
    tag: 'Medical AI',
    tagColor: 'rose',
    image: '/images/ear-cancer.png'
  },
  {
    title: 'TEEOR',
    description: 'AI Builders project - Procurement Checker Tool utilizing OCR + NLP for automated government document verification.',
    tag: 'GovTech',
    tagColor: 'blue',
    image: '/images/teeor.png'
  },
  {
    title: 'Brain Stroke Segmentation',
    description: '3D Reconstruction from CT Scans using U-Net architecture for precise brain stroke analysis and treatment planning.',
    tag: 'Medical Imaging',
    tagColor: 'emerald',
    image: '/images/brain-stroke.png'
  },
  {
    title: 'Satellite Drought Warning',
    description: 'IoT-based satellite system for early drought detection. Winner of GISTDA School Satellite Competition 2024.',
    tag: 'IoT/Space',
    tagColor: 'orange',
    image: '/images/satellite.png'
  },
  {
    title: 'Cansat Rocket System',
    description: 'Complete flight software and deployment system for Thailand Cansat-Rocket Competition. Rocket Consolation Award winner.',
    tag: 'Robotics',
    tagColor: 'cyan',
    image: '/images/cansat.png'
  }
]
</script>

<template>
  <section id="projects" ref="sectionRef" class="py-20">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
      <SectionTitle title="Featured Projects" subtitle="What I've built" />
      
      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
        <ProjectCard
          v-for="(project, index) in projects"
          :key="project.title"
          v-bind="project"
          :class="[
            'transition-all duration-500',
            isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'
          ]"
          :style="{ transitionDelay: `${index * 100}ms` }"
        />
      </div>
    </div>
  </section>
</template>
