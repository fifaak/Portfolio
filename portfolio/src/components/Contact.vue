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

const contactInfo = [
  {
    label: 'Email',
    value: 'pataradany@gmail.com',
    href: 'mailto:pataradany@gmail.com',
    icon: 'M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z'
  },
  {
    label: 'GitHub',
    value: 'github.com/fifaak',
    href: 'https://github.com/fifaak',
    icon: 'M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z'
  },
  {
    label: 'Medium',
    value: 'medium.com/@pataradany',
    href: 'https://medium.com/@pataradany',
    icon: 'M13.54 12a6.8 6.8 0 01-6.77 6.82A6.8 6.8 0 010 12a6.8 6.8 0 016.77-6.82A6.8 6.8 0 0113.54 12zM20.96 12c0 3.54-1.51 6.42-3.38 6.42-1.87 0-3.39-2.88-3.39-6.42s1.52-6.42 3.39-6.42 3.38 2.88 3.38 6.42M24 12c0 3.17-.53 5.75-1.19 5.75-.66 0-1.19-2.58-1.19-5.75s.53-5.75 1.19-5.75C23.47 6.25 24 8.83 24 12z'
  },
  {
    label: 'Location',
    value: 'Bangkok, Thailand',
    href: null,
    icon: 'M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z M15 11a3 3 0 11-6 0 3 3 0 016 0z'
  }
]
</script>

<template>
  <section id="contact" ref="sectionRef" class="py-20">
    <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
      <SectionTitle title="Get In Touch" subtitle="Contact" />
      
      <div
        :class="[
          'text-center transition-all duration-500',
          isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'
        ]"
      >
        <p class="text-slate-300 text-lg mb-10 max-w-2xl mx-auto">
          I'm always open to discussing new projects, opportunities, or collaborations. 
          Feel free to reach out!
        </p>

        <div class="grid sm:grid-cols-2 gap-4 max-w-2xl mx-auto mb-10">
          <a
            v-for="(info, index) in contactInfo"
            :key="info.label"
            :href="info.href || undefined"
            :target="info.href?.startsWith('http') ? '_blank' : undefined"
            rel="noopener noreferrer"
            :class="[
              'flex items-center gap-4 p-4 rounded-xl border transition-all duration-300',
              info.href 
                ? 'bg-slate-800/50 border-slate-700/50 hover:border-primary-500/50 hover:bg-slate-800 cursor-pointer' 
                : 'bg-slate-800/30 border-slate-700/30'
            ]"
            :style="{ transitionDelay: `${index * 100 + 200}ms` }"
          >
            <div class="w-10 h-10 rounded-full bg-primary-500/20 flex items-center justify-center flex-shrink-0">
              <svg class="w-5 h-5 text-primary-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" :d="info.icon" />
              </svg>
            </div>
            <div class="text-left">
              <p class="text-slate-500 text-xs uppercase tracking-wider">{{ info.label }}</p>
              <p class="text-slate-200">{{ info.value }}</p>
            </div>
          </a>
        </div>

        <a
          href="mailto:pataradany@gmail.com"
          class="inline-flex items-center gap-2 px-8 py-3 bg-primary-600 hover:bg-primary-500 text-white font-semibold rounded-lg transition-all duration-300 glow-hover"
        >
          <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
          </svg>
          Send Me an Email
        </a>
      </div>
    </div>

    <!-- Footer -->
    <footer class="mt-20 pt-8 border-t border-slate-800">
      <div class="text-center text-slate-500 text-sm">
        <p>© 2025 Pattaradanai Akkharat. All rights reserved.</p>
        <p class="mt-1">Built with Vue.js & Tailwind CSS</p>
      </div>
    </footer>
  </section>
</template>
