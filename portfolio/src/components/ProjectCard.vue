<script setup lang="ts">
defineProps<{
  title: string
  description: string
  tag: string
  tagColor: string
  image: string
}>()

const tagColors: Record<string, string> = {
  purple: 'bg-purple-500/20 text-purple-400',
  rose: 'bg-rose-500/20 text-rose-400',
  blue: 'bg-blue-500/20 text-blue-400',
  emerald: 'bg-emerald-500/20 text-emerald-400',
  orange: 'bg-orange-500/20 text-orange-400',
  cyan: 'bg-cyan-500/20 text-cyan-400',
}
</script>

<template>
  <div class="group bg-slate-800/50 rounded-xl overflow-hidden border border-slate-700/50 hover:border-primary-500/50 transition-all duration-300 hover:-translate-y-1">
    <!-- Image placeholder -->
    <!-- TODO: Replace placeholder with actual project screenshot -->
    <div class="relative h-48 overflow-hidden">
      <img
        :src="image"
        :alt="title"
        class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-110"
      />
      <div class="absolute inset-0 bg-gradient-to-t from-slate-900/80 to-transparent"></div>
      <span
        :class="[
          'absolute top-4 right-4 px-3 py-1 rounded-full text-xs font-medium',
          tagColors[tagColor] || tagColors.blue
        ]"
      >
        {{ tag }}
      </span>
    </div>
    
    <div class="p-5">
      <h3 class="text-xl font-bold text-white group-hover:text-primary-400 transition-colors">
        {{ title }}
      </h3>
      <p class="text-slate-400 mt-2 text-sm leading-relaxed">
        {{ description }}
      </p>
    </div>
  </div>
</template>
