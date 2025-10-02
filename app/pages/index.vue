<template>
    <main class="p-3 md:px-10 w-screen mx-0 my-auto max-w-0.8">
        <Header />
      <section class="my-auto mx-0 p-5 flex items-center gap-4 md:tracking-medium">
        <Hero />
      </section>
  
      <!-- <section class="container mt-2">
        <p>Testimonials</p>
        <Testimonials />
      </section> -->
  
      <Footer />
    </main>
  </template>
  
  <script setup lang="ts">
  const runtimeConfig = useRuntimeConfig()

  import Hero from '../components/Hero.vue'
  // import Testimonials from '../components/Testimonials.vue'
  import Footer from '../components/Footer.vue'
  import Header from '../components/Header.vue'
  </script>
  
  <style src="~/assets/style.css"></style>