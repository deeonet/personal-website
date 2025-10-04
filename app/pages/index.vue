<template>
    <main class="px-3 lg:px-[10rem] lg:px-[5rem] py-5 w-screen flex justify-between flex-col min-h-screen">
        <Header />
      <section class="my-auto mx-auto p-5 flex items-center gap-4 md:tracking-medium">
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