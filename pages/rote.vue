<template>
  <div class="h-screen w-full bg-[#161616] pt-[2rem]">
    <SpotlightCard  class="my-4 w-[28rem] h-[30rem] text-white ml-[5rem] border-white border-8 " style="background: conic-gradient(from 210deg, #367898 0deg, #3B8DB7 160deg, #2e4f5f 30deg, #29353B 360deg);" spotlightColor="rgba(200, 200, 255, .8)" @click = "show = true">
      <div class="flex flex-col gap-5">
        <NuxtImg src="../public/Screenshot 2025-05-15 102407.png" class="w-full"/>
        <h1 class="font-custom text-[2rem] text-[#f4f4f4]">ElphBlog</h1>
        <div class="flex justify-between">
          <h2>Tech Stack:</h2>
          <p class="text-[.8rem]">Next.JS, JavaScript, Tailwind CSS, <br>
          Firebase Auth, Firestore, Framer Motion</p>
        </div>
      </div>
    </SpotlightCard>
    <div v-if="show" class="fixed bg-black/50 min-h-screen z-10 w-screen flex justify-center items-center top-0 left-0 text-white" @click="show = false">
      <p>2 fished</p>
    </div>
  </div>
  

</template>

<script setup>
import { ref, onMounted } from 'vue';
import TiltedCard from '../components/FixedTitledCard.vue';

const show = ref(false)
</script>
