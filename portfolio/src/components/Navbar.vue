<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)
const isMobileMenuOpen = ref(false)

const navLinks = [
  { name: 'About', href: '#about' },
  { name: 'Experience', href: '#experience' },
  { name: 'Awards', href: '#awards' },
  { name: 'Projects', href: '#projects' },
  { name: 'Contact', href: '#contact' }
]

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <nav
    :class="[
      'fixed top-0 left-0 right-0 z-50 transition-all duration-300',
      isScrolled ? 'bg-slate-950/95 backdrop-blur-md shadow-lg' : 'bg-transparent'
    ]"
  >
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex items-center justify-between h-16">
        <!-- Logo -->
        <a href="#" class="text-xl font-bold gradient-text">PA</a>

        <!-- Desktop Nav -->
        <div class="hidden md:flex items-center gap-6">
          <a
            v-for="link in navLinks"
            :key="link.name"
            :href="link.href"
            class="text-sm text-slate-400 hover:text-white transition-colors"
          >
            {{ link.name }}
          </a>
        </div>

        <!-- Mobile Menu Button -->
        <button
          @click="isMobileMenuOpen = !isMobileMenuOpen"
          class="md:hidden p-2 text-slate-300"
        >
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              :d="isMobileMenuOpen ? 'M6 18L18 6M6 6l12 12' : 'M4 6h16M4 12h16M4 18h16'"
            />
          </svg>
        </button>
      </div>
    </div>

    <!-- Mobile Menu -->
    <div v-if="isMobileMenuOpen" class="md:hidden bg-slate-900/95 backdrop-blur-md border-t border-slate-800">
      <div class="px-4 py-4 space-y-2">
        <a
          v-for="link in navLinks"
          :key="link.name"
          :href="link.href"
          @click="isMobileMenuOpen = false"
          class="block px-4 py-2 text-slate-300 hover:text-white rounded-lg hover:bg-slate-800/50"
        >
          {{ link.name }}
        </a>
      </div>
    </div>
  </nav>
</template>
