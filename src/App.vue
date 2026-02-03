<template>
  <div class="min-h-screen bg-jrd-dark text-white font-body selection:bg-jrd-neon selection:text-black overflow-hidden relative">
    <LoadingScreen />

    <!-- Background Elements -->
    <div class="fixed inset-0 z-0 pointer-events-none">
      <div class="absolute top-0 right-0 w-1/2 h-1/2 bg-gradient-to-b from-jrd-red/20 to-transparent blur-3xl opacity-30"></div>
      <div class="absolute bottom-0 left-0 w-1/2 h-1/2 bg-gradient-to-t from-jrd-neon/10 to-transparent blur-3xl opacity-20"></div>
      <!-- Grid Pattern -->
      <div class="absolute inset-0 bg-[url('https://grainy-gradients.vercel.app/noise.svg')] opacity-20"></div>
      <div class="absolute inset-0" style="background-image: radial-gradient(#333 1px, transparent 1px); background-size: 30px 30px; opacity: 0.1;"></div>
    </div>

    <!-- Navbar -->
    <nav class="relative z-40 px-6 py-4 flex justify-between items-center border-b border-white/10 backdrop-blur-md bg-black/50">
      <div class="flex items-center space-x-2">
        <div class="text-2xl font-racing font-bold italic text-white">
          <span class="text-white drop-shadow-[0_0_8px_rgba(255,255,255,0.5)]">JRD</span> <span class="text-jrd-purple drop-shadow-[0_0_8px_rgba(147,51,234,0.5)]">STORE</span>
        </div>
      </div>
      <div class="flex space-x-4">
        <a :href="contacts.tiktok" target="_blank" class="hover:text-jrd-purple transition-colors duration-300"><i class="fab fa-tiktok"></i> TikTok</a>
        <a :href="contacts.discord" target="_blank" class="hover:text-blue-400 transition-colors duration-300"><i class="fab fa-discord"></i> Discord</a>
      </div>
    </nav>

    <!-- Main Content -->
    <main class="relative z-10 container mx-auto px-4 py-8">
      
      <!-- Header -->
      <header class="text-center mb-12" data-aos="fade-down">
        <h1 class="text-5xl md:text-7xl font-racing font-black italic mb-2 tracking-tighter">
          <span class="text-white">FAST</span> <span class="animate-glow-text text-jrd-purple">DELIVERY</span>
        </h1>
        <p class="text-gray-400 text-lg md:text-xl max-w-2xl mx-auto">
          Top up Robux & Gamepass Termurah, Aman, dan Tercepat. Tema Balap & Elegansi.
        </p>
      </header>

      <!-- Filters -->
      <div class="flex flex-wrap justify-center gap-4 mb-12">
        <button 
          v-for="cat in ['all', 'robux', 'gamepass', 'money']" 
          :key="cat"
          @click="filter = cat"
          class="px-8 py-3 rounded-full font-racing font-bold uppercase tracking-wider transition-all duration-300 border border-white/10 backdrop-blur-sm"
          :class="filter === cat ? 'bg-jrd-purple text-white shadow-[0_0_20px_rgba(147,51,234,0.5)] scale-105' : 'bg-white/5 text-gray-400 hover:bg-white/10 hover:text-white'"
        >
          {{ cat }}
        </button>
      </div>

      <!-- Content Grid -->
      <div class="min-h-[50vh]">
        
        <!-- Robux Grid -->
        <div v-if="filter === 'all' || filter === 'robux'" class="mb-16">
          <h2 v-if="filter === 'all'" class="text-3xl font-racing font-black text-white mb-6 pl-4 border-l-4 border-jrd-purple animate-glow-text tracking-wide">ROBUX LIST (VIA LOGIN)</h2>
          <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4">
            <div 
              v-for="(item, index) in robuxList" 
              :key="item.amount"
              class="group relative bg-white/5 border border-white/10 rounded-xl overflow-hidden hover:border-jrd-purple/50 hover:bg-white/10 transition-all duration-300 hover:-translate-y-1 cursor-pointer"
            >
              <div class="absolute inset-0 bg-gradient-to-br from-jrd-purple/20 to-transparent opacity-0 group-hover:opacity-100 transition-opacity"></div>
              <div class="p-6 text-center transform transition-transform group-hover:scale-105">
                <div class="text-jrd-light-purple font-racing text-3xl font-bold mb-2 drop-shadow-lg">{{ item.amount }} R$</div>
                <div class="text-gray-300 font-bold text-lg">IDR {{ item.price }}</div>
                <a :href="contacts.tiktok" target="_blank" class="block text-center mt-4 w-full py-2 bg-white/10 hover:bg-jrd-purple hover:text-white rounded text-sm font-bold uppercase tracking-wide transition-colors">
                  Beli
                </a>
              </div>
            </div>
          </div>
        </div>

        <!-- Gamepass Grid -->
        <div v-if="filter === 'all' || filter === 'gamepass'">
          <h2 v-if="filter === 'all'" class="text-3xl font-racing font-black text-white mb-6 pl-4 border-l-4 border-jrd-purple animate-glow-text tracking-wide">GAMEPASS LIST</h2>
          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
            <div 
              v-for="(item, index) in gamepassList" 
              :key="item.name"
              class="group relative bg-gradient-to-b from-gray-900 to-black border border-gray-800 rounded-2xl overflow-hidden hover:border-jrd-purple transition-all duration-300 hover:shadow-[0_0_30px_rgba(147,51,234,0.3)]"
            >
              <!-- Card Header -->
              <div class="h-32 bg-gray-900/50 flex items-center justify-center relative overflow-hidden">
                <!-- Decorative Circle -->
                <div class="absolute w-24 h-24 rounded-full bg-jrd-purple/20 blur-xl"></div>
                <!-- Icon Placeholder -->
                 <i :class="item.icon" class="text-5xl text-jrd-light-purple drop-shadow-[0_0_10px_rgba(216,180,254,0.5)]"></i>
              </div>
              
              <div class="p-6 relative">
                 <h3 class="text-xl font-bold font-racing text-white mb-1">{{ item.name }}</h3>
                 <div class="flex items-center space-x-2 mb-4">
                   <span class="px-2 py-0.5 rounded bg-purple-900/50 text-purple-200 text-xs font-bold border border-purple-500/30">GAMEPASS</span>
                 </div>
                 
                 <div class="flex justify-between items-end border-t border-white/10 pt-4">
                   <div>
                     <div class="text-xs text-gray-500 uppercase font-bold">Price (Robux)</div>
                     <div class="text-jrd-light-purple font-mono text-xl">{{ item.priceRobux }} R$</div>
                   </div>
                   <div class="text-right">
                      <div class="text-xs text-gray-500 uppercase font-bold">Est. IDR</div>
                      <div class="text-white font-bold text-xl">{{ item.priceIdr }}</div>
                   </div>
                 </div>
                 
                 <a :href="contacts.tiktok" target="_blank" class="block mt-4 text-center py-3 bg-jrd-purple text-white font-black font-racing uppercase rounded hover:bg-purple-500 transition-colors shadow-lg shadow-purple-900/20">
                   ORDER NOW
                 </a>
              </div>
            </div>
          </div>
        </div>

        <!-- Money Grid -->
        <div v-if="filter === 'all' || filter === 'money'">
          <h2 v-if="filter === 'all'" class="text-3xl font-racing font-black text-white mb-6 pl-4 border-l-4 border-jrd-purple mt-8 animate-glow-text tracking-wide">MONEY LIST</h2>
          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
            <div 
              v-for="(item, index) in moneyList" 
              :key="item.name"
              class="group relative bg-gradient-to-b from-gray-900 to-black border border-gray-800 rounded-2xl overflow-hidden hover:border-jrd-purple transition-all duration-300 hover:shadow-[0_0_30px_rgba(147,51,234,0.3)]"
            >
              <!-- Card Header -->
              <div class="h-32 bg-gray-900/50 flex items-center justify-center relative overflow-hidden">
                <!-- Decorative Circle -->
                <div class="absolute w-24 h-24 rounded-full bg-jrd-purple/20 blur-xl"></div>
                <!-- Icon Placeholder -->
                 <i :class="item.icon" class="text-5xl text-jrd-light-purple drop-shadow-[0_0_10px_rgba(216,180,254,0.5)]"></i>
              </div>
              
              <div class="p-6 relative">
                 <h3 class="text-xl font-bold font-racing text-white mb-1">{{ item.name }}</h3>
                 <div class="flex items-center space-x-2 mb-4">
                   <span class="px-2 py-0.5 rounded bg-green-900/50 text-green-400 text-xs font-bold border border-green-500/30">MONEY</span>
                 </div>
                 
                 <div class="flex justify-between items-end border-t border-white/10 pt-4">
                   <div>
                     <div class="text-xs text-gray-500 uppercase font-bold">Price (Robux)</div>
                     <div class="text-jrd-light-purple font-mono text-xl">{{ item.priceRobux }} R$</div>
                   </div>
                   <div class="text-right">
                      <div class="text-xs text-gray-500 uppercase font-bold">Est. IDR</div>
                      <div class="text-white font-bold text-xl">{{ item.priceIdr }}</div>
                   </div>
                 </div>
                 
                 <a :href="contacts.tiktok" target="_blank" class="block mt-4 text-center py-3 bg-jrd-purple text-white font-black font-racing uppercase rounded hover:bg-purple-500 transition-colors shadow-lg shadow-purple-900/20">
                   ORDER NOW
                 </a>
              </div>
            </div>
          </div>
        </div>

      </div>

    </main>

    <!-- Footer -->
    <footer class="relative z-10 border-t border-white/10 bg-black/80 backdrop-blur text-center py-8 mt-12">
      <p class="font-racing text-gray-500">© 2026 JRD STORE. Racing to the Top.</p>
    </footer>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { robuxList, gamepassList, moneyList, contacts } from './data.js'
import LoadingScreen from './components/LoadingScreen.vue'

const filter = ref('all')
</script>

<style>
/* Custom animations if needed */
</style>
