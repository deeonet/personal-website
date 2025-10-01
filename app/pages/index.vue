<template>
    <main>
      <section class="container header-hero">
        <Hero />
      </section>
  
      <section class="container mt-2">
        <p>Testimonials</p>
        <Testimonials />
      </section>
  
      <Footer />
    </main>
  </template>
  
  <script setup lang="ts">
  const runtimeConfig = useRuntimeConfig()

  import Hero from '../components/Hero.vue'
  import Testimonials from '../components/Testimonials.vue'
  import Footer from '../components/Footer.vue'
  </script>
  
  <style src="~/assets/style.css"></style>