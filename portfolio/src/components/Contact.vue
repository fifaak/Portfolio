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
    icon: 'M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 00-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0020 4.77 5.07 5.07 0 0019.91 1S18.73.65 16 2.48a13.38 13.38 0 00-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 005 4.77a5.44 5.44 0 00-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 009 18.13V22'
  },
  {
    label: 'Medium',
    value: 'medium.com/@pataradany',
    href: 'https://medium.com/@pataradany',
    icon: 'M19 20H5a2 2 0 01-2-2V6a2 2 0 012-2h10a2 2 0 012 2v1m2 13a2 2 0 01-2-2V7m2 13a2 2 0 002-2V9a2 2 0 00-2-2h-2m-4-3H9M7 16h6M7 8h6v4H7V8z'
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
