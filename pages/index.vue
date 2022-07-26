<template>
  <main>
    <section id="hero" class="px-[7%] py-14 flex justify-between items-start">
      <div class="max-w-[700px] space-y-12 self-center">
        <div class="flex space-x-6">
          <div class="rounded-full w-[3.4rem] h-[3.4rem] bg-white p-2 flex items-center justify-center shadow-xl">
            <img src="~assets/imgs/uofl_eagle.svg" class="w-[95%]" alt="University of Louisville Eagle">
          </div>
          <img src="~assets/imgs/uofl_logo.svg" width="70" alt="University of Louisville Logo">
        </div>
        <div class="space-y-10 text-white">
          <h1>Predict <span class="font-normal text-[.88em] block">Dropout Chances</span></h1>
          <p class="max-w-[550px]">See the probability of a student dropping out with powerful insights on ways to improve that probability powered by advanced AI and ML.</p>
          <nuxt-link to="/app" class="cta">Get Started</nuxt-link>
        </div>
      </div>
      <button @click="toggleAbout()" id="about" class="flex items-center px-3 py-2 space-x-2 text-white bg-black rounded-md bg-opacity-30">
        <img src="~assets/imgs/icons/info.svg" width="18" alt="">
        <span class="leading-[0] text-xs">About</span>
      </button>
      <div id="about-modal" class="overlay invisible opacity-0 absolute top-0 left-0 right-0 bottom-0 !overflow-hidden flex items-center justify-center bg-black bg-opacity-0" :class="{show : showAbout}">
        <div class="absolute top-0 left-0 right-0 bottom-0 padding-top" @click="showAbout = false"></div>
        <div class="relative max-w-sm pt-0 content text-white transition-all duration-500 opacity-30 scale-90 bg-black bg-opacity-50 back-blur rounded-xl shadow-2xl">
          <button @click="showAbout = false" aria-label="Close" class="absolute p-2 right-3 top-3">
            <img src="~assets/imgs/icons/x.svg" width="15" alt="">
          </button>
          <h2 class="p-2 text-center rounded-xl rounded-b-none bg-black bg-opacity-40 !font-normal">About</h2>
          <p class="px-7 py-5 text-[.9em]">This is a project by Team 3, College of Business, Masters of Business Analytics, University of Louisville, Class of 2023</p>
        </div>
      </div>
    </section>
  </main>
</template>

<script setup>
  import { ref } from 'vue';
  const showAbout = ref(false)

  function toggleAbout() {
    showAbout.value = !showAbout.value;
  }
</script>

<style scoped>
  #hero {
    @apply bg-cover bg-center bg-no-repeat bg-red;
    min-height: 100vh;
    background-image: 
      linear-gradient(to right, rgb(0, 0, 0), rgba(0, 0, 0, 0) 80%),
      linear-gradient(to right, rgb(0, 0, 0, .4), rgba(0, 0, 0, 0) 80%),
      url("~/assets/imgs/students.jpg");
  }

  h1 {
    @apply text-[3.5em];
    font-family: 'montserrat alternates', sans-serif;
  }

  h2 {
    @apply text-[1.5em]
  }

  #about {
    backdrop-filter: blur(10px);
  }

  #about-modal {
    @apply transition-all ease-in-out duration-300;
    backdrop-filter: blur(10px);
  }

  #about-modal.show {
    @apply opacity-100 visible;
  }

  #about-modal .content {
    transition-timing-function: cubic-bezier(0, 0.55, 0, 1.78);
  }

  .show .content {
    @apply scale-100 opacity-100;
  }
</style>