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
    { threshold: 0.2 }
  )
  
  if (sectionRef.value) {
    observer.observe(sectionRef.value)
  }
})

const stats = [
  { icon: '🚀', value: '1', label: 'Startup Founded', suffix: '' },
  { icon: '🏆', value: '15', label: 'Awards Won', suffix: '+' },
  { icon: '📊', value: '6', label: 'AI Projects', suffix: '+' },
  { icon: '👥', value: '50', label: 'People Mentored', suffix: '+' },
]
</script>

<template>
  <section id="about" ref="sectionRef" class="py-20 bg-slate-900/50">
    <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
      <SectionTitle title="About Me" subtitle="Who I am" />
      
      <div
        :class="[
          'transition-all duration-700',
          isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'
        ]"
      >
        <p class="text-lg text-slate-300 leading-relaxed text-center mb-10">
          Proven track record of co-founding a healthtech startup and leading cross-functional teams 
          to deliver award-winning AI solutions. Skilled in Agile frameworks, full-stack development, 
          and model deployment. Committed to driving innovation through data-driven decision-making.
        </p>

        <div class="grid grid-cols-2 md:grid-cols-4 gap-4 mb-12">
          <div
            v-for="(stat, index) in stats"
            :key="stat.label"
            :class="[
              'bg-slate-800/50 rounded-xl p-5 text-center border border-slate-700/50 hover:border-primary-500/50 transition-all duration-300 hover:-translate-y-1',
              isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'
            ]"
            :style="{ transitionDelay: `${index * 100 + 200}ms` }"
          >
            <span class="text-3xl mb-3 block">{{ stat.icon }}</span>
            <span class="text-3xl font-bold gradient-text">{{ stat.value }}{{ stat.suffix }}</span>
            <span class="text-sm text-slate-400 block mt-1">{{ stat.label }}</span>
          </div>
        </div>

        <!-- YouTube Video -->
        <div
          :class="[
            'flex justify-center transition-all duration-700',
            isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'
          ]"
          :style="{ transitionDelay: '600ms' }"
        >
          <div class="relative rounded-2xl overflow-hidden border border-slate-700/50 shadow-2xl glow">
            <iframe
              src="https://www.youtube.com/embed/zfeK9vn1h48?autoplay=1&mute=1&loop=1&playlist=zfeK9vn1h48"
              title="About Me Video"
              width="315"
              height="560"
              frameborder="0"
              allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
              allowfullscreen
              class="block"
            ></iframe>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
