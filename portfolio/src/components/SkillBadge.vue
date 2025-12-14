<script setup lang="ts">
defineProps<{
  name: string
  color: string
}>()

const colorClasses: Record<string, string> = {
  emerald: 'bg-emerald-500/10 text-emerald-400 border-emerald-500/30',
  blue: 'bg-blue-500/10 text-blue-400 border-blue-500/30',
  purple: 'bg-purple-500/10 text-purple-400 border-purple-500/30',
  orange: 'bg-orange-500/10 text-orange-400 border-orange-500/30',
  cyan: 'bg-cyan-500/10 text-cyan-400 border-cyan-500/30',
}
</script>

<template>
  <span
    :class="[
      'px-4 py-2 rounded-full text-sm font-medium border transition-all duration-300 hover:scale-105',
      colorClasses[color] || colorClasses.blue
    ]"
  >
    {{ name }}
  </span>
</template>
