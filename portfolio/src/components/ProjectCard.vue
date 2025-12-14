<script setup lang="ts">
defineProps<{
  title: string
  description: string
  tag: string
  tagColor: string
  image: string
  tech: string[]
  year: string
  role: string
  link?: string
}>()

const tagColors: Record<string, string> = {
  purple: 'bg-purple-500/20 text-purple-400 border-purple-500/30',
  rose: 'bg-rose-500/20 text-rose-400 border-rose-500/30',
  blue: 'bg-blue-500/20 text-blue-400 border-blue-500/30',
  emerald: 'bg-emerald-500/20 text-emerald-400 border-emerald-500/30',
  orange: 'bg-orange-500/20 text-orange-400 border-orange-500/30',
  cyan: 'bg-cyan-500/20 text-cyan-400 border-cyan-500/30'
}
</script>

<template>
  <a
    :href="link"
    :target="link ? '_blank' : undefined"
    :rel="link ? 'noopener noreferrer' : undefined"
    class="group bg-slate-800/50 rounded-2xl overflow-hidden border border-slate-700/50 hover:border-primary-500/50 transition-all duration-300 hover:-translate-y-2 hover:shadow-xl hover:shadow-primary-500/10 block"
    :class="{ 'cursor-pointer': link }"
  >
    <!-- Image -->
    <div class="relative h-48 overflow-hidden">
      <img
        :src="image"
        :alt="title"
        class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-110"
      />
      <div class="absolute inset-0 bg-gradient-to-t from-slate-900 via-slate-900/50 to-transparent"></div>

      <!-- Tag -->
      <span
        :class="[
          'absolute top-4 right-4 px-3 py-1 rounded-full text-xs font-medium border',
          tagColors[tagColor] || tagColors.blue
        ]"
      >
        {{ tag }}
      </span>

      <!-- Year Badge -->
      <span
        class="absolute top-4 left-4 px-2 py-1 rounded-md bg-slate-900/80 text-slate-300 text-xs font-medium backdrop-blur-sm"
      >
        {{ year }}
      </span>

      <!-- Role overlay on hover -->
      <div
        class="absolute bottom-0 left-0 right-0 p-4 translate-y-full group-hover:translate-y-0 transition-transform duration-300"
      >
        <span class="text-xs text-primary-400 font-medium">{{ role }}</span>
      </div>
    </div>

    <!-- Content -->
    <div class="p-5">
      <h3
        class="text-lg font-bold text-white group-hover:text-primary-400 transition-colors line-clamp-1"
      >
        {{ title }}
      </h3>
      <p class="text-slate-400 mt-2 text-sm leading-relaxed line-clamp-2">
        {{ description }}
      </p>

      <!-- Tech Stack -->
      <div class="flex flex-wrap gap-1.5 mt-4">
        <span
          v-for="t in tech.slice(0, 4)"
          :key="t"
          class="px-2 py-1 bg-slate-700/50 text-slate-300 text-xs rounded-md"
        >
          {{ t }}
        </span>
      </div>

      <!-- Action -->
      <div class="mt-4 pt-4 border-t border-slate-700/50 flex items-center justify-between">
        <span class="text-xs text-slate-500">Click to view details</span>
        <div
          class="w-8 h-8 rounded-full bg-primary-500/10 flex items-center justify-center text-primary-400 group-hover:bg-primary-500 group-hover:text-white transition-all duration-300"
        >
          <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M9 5l7 7-7 7"
            />
          </svg>
        </div>
      </div>
    </div>
  </a>
</template>
