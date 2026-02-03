<template>
  <div v-if="loading" class="fixed inset-0 z-50 flex flex-col items-center justify-center bg-black transition-opacity duration-700" :class="{ 'opacity-0 pointer-events-none': !visible }">
    <div class="relative flex items-center justify-center">
      <!-- Circuit / Speedometer Effect -->
      <div class="absolute w-[350px] h-[350px] md:w-[500px] md:h-[500px] border-2 border-jrd-neon/30 rounded-full animate-spin-fast border-t-jrd-neon border-r-transparent border-b-jrd-neon border-l-transparent"></div>
      <div class="absolute w-[280px] h-[280px] md:w-[400px] md:h-[400px] border-2 border-red-600/30 rounded-full animate-spin-fast border-t-transparent border-r-red-600 border-b-transparent border-l-red-600" style="animation-direction: reverse; animation-duration: 3s;"></div>

      <!-- Brand Name -->
      <h1 class="relative z-10 text-5xl md:text-7xl font-racing font-black text-transparent bg-clip-text bg-gradient-to-r from-red-600 via-jrd-neon to-red-600 animate-pulse tracking-wider text-center drop-shadow-[0_0_15px_rgba(255,0,0,0.5)] px-4">
        JRD STORE
      </h1>
    </div>
    
    <div class="mt-8 flex items-center space-x-2">
      <div class="w-3 h-3 bg-red-600 rounded-full animate-bounce"></div>
      <div class="w-3 h-3 bg-yellow-500 rounded-full animate-bounce delay-100"></div>
      <div class="w-3 h-3 bg-green-500 rounded-full animate-bounce delay-200"></div>
    </div>
    
    <p class="mt-4 text-gray-500 font-racing tracking-widest text-sm">START YOUR ENGINE...</p>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const loading = ref(true)
const visible = ref(true)

onMounted(() => {
  // Always show for at least 2.5 seconds to simulate "Setup"
  setTimeout(() => {
    visible.value = false
    setTimeout(() => {
      loading.value = false
    }, 700) // Wait for fade out
  }, 2500)
})
</script>

<style scoped>
.delay-100 {
  animation-delay: 0.1s;
}
.delay-200 {
  animation-delay: 0.2s;
}
</style>
