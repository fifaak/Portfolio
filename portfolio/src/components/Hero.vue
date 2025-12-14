<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const isDropdownOpen = ref(false)
const dropdownRef = ref<HTMLElement | null>(null)

const closeDropdown = (e: MouseEvent) => {
  if (dropdownRef.value && !dropdownRef.value.contains(e.target as Node)) {
    isDropdownOpen.value = false
  }
}

onMounted(() => {
  document.addEventListener('click', closeDropdown)
})

onUnmounted(() => {
  document.removeEventListener('click', closeDropdown)
})

const profileLinks = [
  { name: 'CV / Resume', url: 'https://www.canva.com/design/DAGRkGApn6w/NxPCu4jbKOs8oFhKhJsYqQ/view' },
  { name: 'High School Portfolio', url: 'https://www.canva.com/design/DAG7eN6jOc4/qOgTMTfTQrwibkzgJdT5uw/view' }
]

const socialLinks = [
  {
    name: 'GitHub',
    url: 'https://github.com/fifaak',
    icon: 'M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z'
  },
  {
    name: 'Medium',
    url: 'https://medium.com/@pataradany',
    icon: 'M13.54 12a6.8 6.8 0 01-6.77 6.82A6.8 6.8 0 010 12a6.8 6.8 0 016.77-6.82A6.8 6.8 0 0113.54 12zM20.96 12c0 3.54-1.51 6.42-3.38 6.42-1.87 0-3.39-2.88-3.39-6.42s1.52-6.42 3.39-6.42 3.38 2.88 3.38 6.42M24 12c0 3.17-.53 5.75-1.19 5.75-.66 0-1.19-2.58-1.19-5.75s.53-5.75 1.19-5.75C23.47 6.25 24 8.83 24 12z'
  },
  {
    name: 'Email',
    url: 'mailto:pataradany@gmail.com',
    icon: 'M20 4H4c-1.1 0-1.99.9-1.99 2L2 18c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z'
  }
]
</script>

<template>
  <section class="min-h-screen flex items-center justify-center relative overflow-hidden pt-16">
    <!-- Banner Background -->
    <div class="absolute inset-0">
      <img 
        src="/images/profile/banner.jpg" 
        alt="Banner" 
        class="w-full h-full object-cover"
      />
      <div class="absolute inset-0 bg-slate-950/70"></div>
    </div>
    <!-- Background gradient overlay -->
    <div class="absolute inset-0 bg-gradient-to-br from-slate-950/80 via-slate-900/60 to-primary-950/50"></div>
    <div class="absolute top-1/4 -left-1/4 w-96 h-96 bg-primary-600/20 rounded-full blur-3xl"></div>
    <div class="absolute bottom-1/4 -right-1/4 w-96 h-96 bg-purple-600/20 rounded-full blur-3xl"></div>
    
    <div class="relative z-10 max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
      <!-- Profile Image -->
      <div class="fade-in mb-8">
        <div class="w-36 h-36 mx-auto rounded-full bg-gradient-to-br from-primary-500 to-purple-600 p-1 glow">
          <img 
            src="/images/profile/profile.jpg" 
            alt="Pattaradanai Akkharat"
            class="w-full h-full rounded-full object-cover"
          />
        </div>
      </div>

      <h1 class="fade-in delay-100 text-4xl sm:text-5xl lg:text-6xl font-bold mb-4">
        <span class="gradient-text">Pattaradanai Akkharat</span>
      </h1>
      
      <p class="fade-in delay-200 text-xl sm:text-2xl text-slate-300 mb-4 font-medium">
        Project Manager | Data Scientist | System Analyst
      </p>
      
      <p class="fade-in delay-300 text-lg text-slate-400 max-w-2xl mx-auto mb-8">
        First-year Computer Engineering student bridging the gap between complex technical requirements and business objectives.
      </p>

      <!-- CTA Buttons -->
      <div class="fade-in delay-400 flex flex-col sm:flex-row items-center justify-center gap-4 mb-10 relative z-20">
        <a
          href="#experience"
          class="px-8 py-3 bg-primary-600 hover:bg-primary-500 text-white font-semibold rounded-lg transition-all duration-300 glow-hover"
        >
          View Experience
        </a>
        <div ref="dropdownRef" class="relative z-[100]">
          <button
            @click.stop="isDropdownOpen = !isDropdownOpen"
            class="px-8 py-3 border border-primary-500 text-primary-400 hover:bg-primary-500/10 font-semibold rounded-lg transition-all duration-300 flex items-center gap-2"
          >
            See More Profile
            <svg
              :class="['w-4 h-4 transition-transform', isDropdownOpen ? 'rotate-180' : '']"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
            </svg>
          </button>
          <div
            v-if="isDropdownOpen"
            class="absolute top-full mt-2 left-0 right-0 rounded-lg overflow-hidden shadow-2xl z-[9999]"
            style="background-color: #1e293b;"
          >
            <a
              v-for="link in profileLinks"
              :key="link.name"
              :href="link.url"
              target="_blank"
              rel="noopener noreferrer"
              class="block px-4 py-3 text-white hover:bg-primary-600 transition-colors text-sm font-medium border-b border-slate-700 last:border-b-0"
            >
              {{ link.name }}
            </a>
          </div>
        </div>
      </div>

      <!-- Social Links -->
      <div class="fade-in delay-500 flex items-center justify-center gap-6 relative z-10">
        <a
          v-for="social in socialLinks"
          :key="social.name"
          :href="social.url"
          target="_blank"
          rel="noopener noreferrer"
          class="text-slate-400 hover:text-primary-400 transition-colors duration-300"
          :aria-label="social.name"
        >
          <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24">
            <path :d="social.icon" />
          </svg>
        </a>
      </div>

      <!-- Scroll indicator -->
      <div class="absolute bottom-8 left-1/2 -translate-x-1/2 animate-bounce">
        <svg class="w-6 h-6 text-slate-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m7 7V3" />
        </svg>
      </div>
    </div>
  </section>
</template>
