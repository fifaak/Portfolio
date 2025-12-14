<script setup lang="ts">
import Hero from './components/Hero.vue'
import AwardsMarquee from './components/AwardsMarquee.vue'
import About from './components/About.vue'
import Skills from './components/Skills.vue'
import Experience from './components/Experience.vue'
import Projects from './components/Projects.vue'
import Awards from './components/Awards.vue'
import Contact from './components/Contact.vue'
import Navbar from './components/Navbar.vue'
</script>

<template>
  <div class="min-h-screen bg-slate-950">
    <Navbar />
    <main>
      <Hero />
      <AwardsMarquee />
      <About />
      <Experience />
      <Skills />
      <Awards />
      <Projects />
      <Contact />
    </main>
  </div>
</template>
