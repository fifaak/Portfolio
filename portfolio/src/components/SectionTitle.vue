<script setup lang="ts">
defineProps<{
  title: string
  subtitle?: string
}>()
</script>

<template>
  <div class="text-center mb-12">
    <span v-if="subtitle" class="text-primary-400 text-sm font-semibold uppercase tracking-wider">
      {{ subtitle }}
    </span>
    <h2 class="text-3xl sm:text-4xl font-bold text-white mt-2">
      {{ title }}
    </h2>
    <div class="w-20 h-1 bg-gradient-to-r from-primary-500 to-purple-500 mx-auto mt-4 rounded-full"></div>
  </div>
</template>
