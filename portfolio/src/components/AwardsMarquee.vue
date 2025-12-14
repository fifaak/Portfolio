<script setup lang="ts">
const awards = [
  '🥉 SuperAI Engineer SS5 - Bronze Medal',
  '🏆 GISTDA Satellite Competition - 1st Place',
  '🥈 Siriraj Hackathon 2023 - 2nd Runner-up',
  '🌏 Global Youth Entrepreneurship - Top 10 Global',
  '⭐ AI Builders 3 - Outstanding Project',
  '💰 TechBite 5.0 - 850,000 THB Funding',
  '🏅 Thailand ICT Award 2024 - Finalist',
  '🥈 Mental Health Hackathon - 1st Runner-up',
  '🚀 Typhoon Hackathon - Top 12 Finalist'
]
</script>

<template>
  <div class="bg-gradient-to-r from-primary-900/50 via-purple-900/50 to-primary-900/50 py-3 overflow-hidden border-y border-primary-500/20">
    <div class="marquee-container">
      <div class="marquee-content">
        <span v-for="(award, i) in awards" :key="i" class="mx-8 text-sm text-slate-300 whitespace-nowrap">
          {{ award }}
        </span>
        <span v-for="(award, i) in awards" :key="'dup-' + i" class="mx-8 text-sm text-slate-300 whitespace-nowrap">
          {{ award }}
        </span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.marquee-container {
  width: 100%;
  overflow: hidden;
}

.marquee-content {
  display: flex;
  animation: marquee 30s linear infinite;
}

@keyframes marquee {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-50%);
  }
}

.marquee-content:hover {
  animation-play-state: paused;
}
</style>
