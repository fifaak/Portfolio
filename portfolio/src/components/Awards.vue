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

const awards = [
  {
    title: 'SuperAI Engineer SS5',
    achievement: 'Bronze Medal & Outstanding Poster',
    logo: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSA4onbPkuhkcJIM4SDi9eGWZOs3MT6yCm_xw&s',
    highlight: true
  },
  {
    title: 'Siriraj Hackathon 2023',
    achievement: '2nd Runner-up (420 teams → Top 10)',
    logo: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRkmG7LxM8amn4launEjuFAzDNohKst79t0dA&s',
    highlight: true
  },
  {
    title: 'GISTDA School Satellite Competition 2024',
    achievement: 'Winner (1st Place)',
    logo: 'https://yt3.googleusercontent.com/StU-KSWrVV-iLbCRGbHtDsn_nNGOj3E-p-FrnA5pUY29Vwn-fswXaVJZkp08B4pGAc5X5gjZ=s900-c-k-c0x00ffffff-no-rj',
    highlight: true
  },
  {
    title: 'Thailand ICT Award 2024',
    achievement: 'Finalist - AI R&D Category',
    logo: 'https://www.thaipr.net/wp-content/uploads/2022/07/logo-TICTA-Awards-f75750b4.jpg',
    highlight: false
  },
  {
    title: 'Global Youth Entrepreneurship Challenge 2024',
    achievement: 'Top 10 Global',
    logo: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQmbQDzXTBH_NVOvQpMNs2bwhav6zNlOMftpA&s',
    highlight: true
  },
  {
    title: 'AI Builders 3',
    achievement: 'Outstanding AI Project (500 → 45 teams)',
    logo: 'https://avatars.githubusercontent.com/u/99741955?s=200&v=4',
    highlight: true
  },
  {
    title: 'TechBite 5.0',
    achievement: 'Received 850,000 THB Funding',
    logo: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTMSxRrjZwMMwU22hT-fhu0CSvigaDkbEpM5g&s',
    highlight: false
  },
  {
    title: 'Mental Health Hackathon 2024',
    achievement: '1st Runner-up',
    logo: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTCecsS36duZf54LVGqfWDy7aDyRGT594nquw&s',
    highlight: false
  },
  {
    title: 'Typhoon Hackathon 2024',
    achievement: 'Finalist (84 teams → Top 12)',
    logo: 'https://www.scb10x.com/images/logo.png',
    highlight: false
  }
]
</script>

<template>
  <section id="awards" ref="sectionRef" class="py-20 bg-slate-900/50">
    <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8">
      <SectionTitle title="Awards & Honors" subtitle="Recognition" />

      <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-4">
        <div
          v-for="(award, index) in awards"
          :key="award.title"
          :class="[
            'p-5 rounded-xl border transition-all duration-500 hover:-translate-y-1',
            award.highlight
              ? 'bg-gradient-to-br from-primary-900/30 to-purple-900/30 border-primary-500/30'
              : 'bg-slate-800/50 border-slate-700/50',
            isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'
          ]"
          :style="{ transitionDelay: `${index * 100}ms` }"
        >
          <div class="flex items-start gap-4">
            <div
              class="w-12 h-12 rounded-lg bg-white/10 flex items-center justify-center flex-shrink-0 overflow-hidden"
            >
              <img
                :src="award.logo"
                :alt="award.title"
                class="w-full h-full object-contain"
                @error="($event.target as HTMLImageElement).parentElement!.innerHTML = '🏆'"
              />
            </div>
            <div class="flex-1 min-w-0">
              <h3 class="text-white font-semibold text-sm leading-tight">{{ award.title }}</h3>
              <p class="text-primary-400 text-xs mt-1">{{ award.achievement }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
