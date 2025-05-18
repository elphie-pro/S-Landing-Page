<template>
  <div class="p-8 flex flex-row">
    <h2 class="text-2xl flex items-center">
      <span>I love</span>
      <span class="ml-2"></span>
      <RotatingText 
        :texts="['Vue.js', 'Nuxt', 'Coding']"
        :rotation-interval="3000"
        :stagger-duration="0.05"
        @next="handleTextChange"
        class="text-white bg-blue-500 p-4 text-center h-[4rem] rounded-3xl font-bold min-w-[150px] inline-block "
      />
    </h2>
  </div>
</template>

<script setup>
const handleTextChange = (index) => {
  console.log('Now showing text at index:', index)
}
import { ref, computed, watch, onMounted, onBeforeUnmount, nextTick } from 'vue'
</script>