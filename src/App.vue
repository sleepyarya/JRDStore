<template>
  <div class="h-screen w-screen bg-[#07000d] text-white font-sans overflow-hidden relative flex flex-col items-center" style="transform: translateZ(0);">
    
    <!-- Loading Screen -->
    <Transition name="fade-loading">
      <div v-if="isLoading" class="fixed inset-0 z-50 flex items-center justify-center bg-[#07000d] overflow-hidden" style="will-change: opacity;">
        <!-- Animated Background -->
        <div class="absolute inset-0 flex items-center justify-center pointer-events-none">
           <div class="absolute top-1/4 left-1/4 w-[40vw] h-[40vw] bg-purple-600/20 blur-[120px] rounded-full animate-pulse-fast mix-blend-screen" style="will-change: opacity, transform;"></div>
           <div class="absolute bottom-1/4 right-1/4 w-[30vw] h-[30vw] bg-fuchsia-600/20 blur-[100px] rounded-full animate-pulse-fast-delay mix-blend-screen" style="will-change: opacity, transform;"></div>
        </div>
        
        <div class="relative z-10 flex flex-col items-center gap-6" style="will-change: transform;">
          <i class="fa-solid fa-server text-5xl text-purple-400 animate-bounce drop-shadow-[0_0_15px_rgba(192,132,252,0.8)]"></i>
          <h2 class="text-2xl md:text-4xl font-black italic tracking-[0.2em] text-transparent bg-clip-text bg-gradient-to-r from-purple-400 to-fuchsia-500 animate-pulse drop-shadow-[0_0_15px_rgba(217,70,239,0.5)]">
            LOADING DATABASE DDS
          </h2>
          <!-- Loading Bar -->
          <div class="w-48 md:w-64 h-1.5 bg-white/10 rounded-full overflow-hidden mt-2 relative">
             <div class="absolute top-0 left-0 h-full bg-gradient-to-r from-purple-500 to-fuchsia-500 rounded-full animate-loading-bar" style="will-change: transform;"></div>
          </div>
        </div>
      </div>
    </Transition>

    <!-- Background Glow -->
    <div class="absolute inset-0 pointer-events-none overflow-hidden">
      <div class="absolute top-1/4 left-1/4 w-[500px] h-[500px] bg-purple-600/30 blur-[150px] rounded-full mix-blend-screen animate-pulse-slow" style="will-change: opacity, transform;"></div>
      <div class="absolute bottom-1/4 right-1/4 w-[400px] h-[400px] bg-fuchsia-900/40 blur-[150px] rounded-full mix-blend-screen animate-pulse-slow-delay" style="will-change: opacity, transform;"></div>
    </div>

    <!-- Navbar -->
    <nav class="w-full relative z-40 px-8 py-5 border-b border-purple-500/30 bg-black/50 backdrop-blur-xl flex justify-between items-center shadow-[0_0_30px_rgba(147,51,234,0.2)]" style="will-change: transform;">
      <!-- Left side: DDS E-KTP -->
      <div class="flex items-center">
        <h1 class="text-3xl font-black italic tracking-widest text-white drop-shadow-[0_0_15px_rgba(255,255,255,0.8)] flex items-center gap-2">
          <i class="fa-solid fa-id-card text-purple-400"></i>
          DDS <span class="text-transparent bg-clip-text bg-gradient-to-r from-purple-400 to-fuchsia-500 drop-shadow-[0_0_12px_rgba(217,70,239,0.8)]">E-KTP</span>
        </h1>
      </div>
      
      <!-- Right side menus: 2 Navbars -->
      <div class="flex space-x-4 md:space-x-6">
        <button 
          @click="activeTab = 'biodata'" 
          :class="['px-6 py-2.5 rounded-xl font-black tracking-wide uppercase text-sm transition-all duration-300 border border-transparent shadow-[0_0_15px_transparent] will-change-transform', activeTab === 'biodata' ? 'bg-gradient-to-r from-purple-600 to-fuchsia-600 text-white shadow-[0_0_25px_rgba(192,132,252,0.6)] border-purple-400/50 scale-105' : 'text-purple-200/60 hover:text-white hover:bg-white/10']"
        >
          Biodata
        </button>
        <button 
          @click="activeTab = 'ktp'" 
          :class="['px-6 py-2.5 rounded-xl font-black tracking-wide uppercase text-sm transition-all duration-300 border border-transparent shadow-[0_0_15px_transparent] will-change-transform', activeTab === 'ktp' ? 'bg-gradient-to-r from-purple-600 to-fuchsia-600 text-white shadow-[0_0_25px_rgba(192,132,252,0.6)] border-purple-400/50 scale-105' : 'text-purple-200/60 hover:text-white hover:bg-white/10']"
        >
          KTP
        </button>
      </div>
    </nav>

    <!-- Main Content -->
    <main class="flex-1 w-full max-w-6xl mx-auto flex items-center justify-center p-6 relative z-10">
      
      <!-- BIODATA TAB -->
      <Transition name="fade-scale" mode="out-in">
        <div v-if="activeTab === 'biodata'" class="w-full max-w-4xl flex flex-col md:flex-row bg-black/40 backdrop-blur-2xl border border-purple-500/40 rounded-[2rem] p-8 md:p-14 shadow-[0_0_60px_rgba(147,51,234,0.25)] gap-12 items-center justify-center relative overflow-hidden" style="will-change: transform, opacity;">
          
          <!-- Inner Glow -->
          <div class="absolute -top-32 -right-32 w-64 h-64 bg-fuchsia-600/20 blur-[100px] rounded-full pointer-events-none"></div>
          <div class="absolute -bottom-32 -left-32 w-64 h-64 bg-purple-600/20 blur-[100px] rounded-full pointer-events-none"></div>

          <!-- Profile Image (Full Body) -->
          <div class="relative group z-10 shrink-0">
            <div class="absolute inset-0 bg-gradient-to-tr from-purple-600 to-fuchsia-500 rounded-3xl blur-2xl group-hover:blur-3xl transition duration-500 opacity-60" style="will-change: filter, opacity;"></div>
            <img src="/fullbody.png" alt="Profile Full Body" class="w-56 h-80 md:w-64 md:h-[400px] object-cover object-top rounded-3xl border-[3px] border-white/20 shadow-2xl relative z-10 transform group-hover:scale-[1.02] transition duration-300 will-change-transform" />
          </div>
          
          <!-- Info Info -->
          <div class="flex-1 flex flex-col gap-8 text-center md:text-left z-10 w-full">
            <div>
              <h2 class="text-5xl md:text-7xl font-black text-white mb-3 drop-shadow-[0_0_20px_rgba(255,255,255,0.4)] tracking-tight">JHORDI</h2>
              <span class="inline-flex items-center gap-2 px-5 py-2 rounded-full bg-gradient-to-r from-purple-500/20 to-fuchsia-500/20 border border-purple-400/40 text-purple-200 font-black tracking-widest text-sm shadow-[0_0_15px_rgba(192,132,252,0.3)]">
                <i class="fa-solid fa-user-astronaut"></i> CREW
              </span>
            </div>
            
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-5 w-full">
              <div class="bg-white/5 border border-purple-500/20 rounded-2xl p-6 backdrop-blur-md hover:bg-white/10 hover:border-purple-400/50 transition-all duration-300 group">
                <p class="text-purple-300/70 text-xs font-bold uppercase tracking-widest mb-2 group-hover:text-purple-300 transition-colors">Nomor Induk Kependudukan (NIK)</p>
                <p class="text-3xl font-mono font-black text-white tracking-widest drop-shadow-[0_0_10px_rgba(255,255,255,0.3)]">3321</p>
              </div>
              <div class="bg-white/5 border border-purple-500/20 rounded-2xl p-6 backdrop-blur-md hover:bg-white/10 hover:border-purple-400/50 transition-all duration-300 group">
                <p class="text-purple-300/70 text-xs font-bold uppercase tracking-widest mb-2 group-hover:text-purple-300 transition-colors">Pekerjaan</p>
                <p class="text-2xl font-black text-transparent bg-clip-text bg-gradient-to-r from-purple-300 to-fuchsia-300 drop-shadow-[0_0_10px_rgba(217,70,239,0.5)]">Kurir MBG</p>
              </div>
            </div>

            <!-- Action Buttons -->
            <div class="flex flex-col sm:flex-row gap-4 mt-2 w-full">
              <a href="https://www.tiktok.com/@jhordi3321" target="_blank" class="flex-1 flex items-center justify-center gap-3 py-3 px-6 bg-gradient-to-r from-gray-900 to-black hover:from-black hover:to-gray-900 border border-purple-500/30 hover:border-purple-400/80 rounded-2xl font-bold tracking-widest uppercase transition-all duration-300 shadow-lg hover:shadow-[0_0_20px_rgba(147,51,234,0.4)] group">
                <i class="fa-brands fa-tiktok text-xl text-white group-hover:scale-110 transition-transform"></i>
                <span class="text-white">TikTok</span>
              </a>
              <a href="https://discord.gg/f9caRV8DHh" target="_blank" class="flex-1 flex items-center justify-center gap-3 py-3 px-6 bg-gradient-to-r from-indigo-900/40 to-blue-900/40 hover:from-indigo-600 hover:to-blue-600 border border-blue-500/30 hover:border-blue-400/80 rounded-2xl font-bold tracking-widest uppercase transition-all duration-300 shadow-lg hover:shadow-[0_0_20px_rgba(79,70,229,0.4)] group">
                <i class="fa-brands fa-discord text-xl text-white group-hover:scale-110 transition-transform"></i>
                <span class="text-white">Discord</span>
              </a>
            </div>
          </div>
        </div>

        <!-- KTP TAB -->
        <div v-else-if="activeTab === 'ktp'" class="w-full max-w-3xl flex justify-center perspective-1000" style="will-change: transform, opacity;">
          <!-- KTP Card design -->
          <div class="w-full relative aspect-[1.586/1] bg-gradient-to-br from-[#c4e0ff] via-[#d6e8ff] to-[#a3cfff] rounded-3xl shadow-[0_30px_60px_rgba(147,51,234,0.4),0_0_40px_rgba(217,70,239,0.2)] border-4 border-white/80 overflow-hidden text-[#111] p-6 md:p-10 flex flex-col transform transition-transform hover:rotate-y-2 hover:rotate-x-2 hover:scale-[1.03] duration-300 group will-change-transform">
            
            <!-- Background pattern -->
            <div class="absolute inset-0 opacity-15 pointer-events-none mix-blend-overlay" style="background-image: repeating-linear-gradient(45deg, #000 0, #000 1px, transparent 0, transparent 50%); background-size: 12px 12px; will-change: transform;"></div>
            
            <!-- Hologram Overlay -->
            <div class="absolute inset-0 opacity-0 group-hover:opacity-30 transition-opacity duration-500 pointer-events-none mix-blend-color-dodge bg-gradient-to-tr from-transparent via-purple-300 to-transparent" style="will-change: opacity;"></div>

            <!-- Header -->
            <div class="text-center mb-6 relative z-10 border-b-2 border-black/10 pb-2">
              <h2 class="text-xl md:text-2xl font-black tracking-widest uppercase">PROVINSI JAWA TIMUR</h2>
              <h3 class="text-lg md:text-xl font-bold tracking-wider uppercase">KOTA MALANG</h3>
            </div>
            
            <!-- Body -->
            <div class="flex gap-4 md:gap-8 flex-1 relative z-10">
              <!-- Text Info -->
              <div class="flex-1 flex flex-col text-sm md:text-base font-bold gap-2 md:gap-3 font-mono">
                <div class="flex mt-2 items-center">
                  <span class="w-28 md:w-40 uppercase">NIK</span>
                  <span class="mr-3">:</span>
                  <span class="text-2xl md:text-3xl tracking-[0.2em] font-black text-black">3321</span>
                </div>
                
                <div class="flex mt-3">
                  <span class="w-28 md:w-40 uppercase">Nama</span>
                  <span class="mr-3">:</span>
                  <span class="uppercase">JHORDI</span>
                </div>
                
                <div class="flex">
                  <span class="w-28 md:w-40 uppercase">Status</span>
                  <span class="mr-3">:</span>
                  <span class="uppercase">CREW</span>
                </div>

                <div class="flex">
                  <span class="w-28 md:w-40 uppercase">Pekerjaan</span>
                  <span class="mr-3">:</span>
                  <span class="uppercase">KURIR MBG</span>
                </div>

                <div class="flex">
                  <span class="w-28 md:w-40 uppercase">Kewarganegaraan</span>
                  <span class="mr-3">:</span>
                  <span class="uppercase">WNI</span>
                </div>

                <div class="flex">
                  <span class="w-28 md:w-40 uppercase">Berlaku Hingga</span>
                  <span class="mr-3">:</span>
                  <span class="uppercase">SEUMUR HIDUP</span>
                </div>
              </div>

              <!-- Photo & Signature Area -->
              <div class="w-32 md:w-44 flex flex-col items-center gap-3 shrink-0">
                <!-- Pas Foto Sebatas Dada -->
                <div class="w-full aspect-[3/4] rounded-lg border-2 border-white/50 overflow-hidden bg-gray-400 shadow-xl relative z-10">
                  <img src="/ktp-crop.png" alt="Pas Foto" class="w-full h-full object-cover object-top grayscale-[30%] contrast-110 sepia-[10%] will-change-transform" />
                </div>
                <!-- Signature Loc & Date -->
                <div class="text-[10px] md:text-xs text-center font-bold font-mono uppercase">
                  <div>KOTA MALANG</div>
                  <div>23-12-2025</div>
                </div>
              </div>
            </div>
            
            <!-- Card Glare effect -->
            <div class="absolute -top-[100%] -left-[100%] w-[300%] h-[300%] bg-white/20 transform rotate-45 pointer-events-none group-hover:animate-glare" style="will-change: transform;"></div>
          </div>
        </div>
      </Transition>

    </main>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const activeTab = ref('biodata')
const isLoading = ref(true)

onMounted(() => {
  // Animasi loading screen
  setTimeout(() => {
    isLoading.value = false
  }, 2500)
})
</script>

<style>
/* Optimized Animations for 60/144hz */
.will-change-transform {
  will-change: transform;
}

.fade-loading-enter-active,
.fade-loading-leave-active {
  transition: opacity 0.6s cubic-bezier(0.4, 0, 0.2, 1);
}
.fade-loading-enter-from,
.fade-loading-leave-to {
  opacity: 0;
}

.fade-scale-enter-active,
.fade-scale-leave-active {
  transition: transform 0.4s cubic-bezier(0.34, 1.56, 0.64, 1), opacity 0.4s ease-out;
}
.fade-scale-enter-from {
  opacity: 0;
  transform: scale(0.95) translateY(10px) rotateX(-5deg);
}
.fade-scale-leave-to {
  opacity: 0;
  transform: scale(0.95) translateY(-10px) rotateX(5deg);
}

@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800;900&family=JetBrains+Mono:wght@400;700;800&display=swap');

html, body {
  margin: 0;
  padding: 0;
  overflow: hidden;
  background-color: #07000d;
}

.font-sans {
  font-family: 'Inter', sans-serif;
}
.font-mono {
  font-family: 'JetBrains Mono', monospace;
}

.perspective-1000 {
  perspective: 1000px;
}
.rotate-y-2 {
  transform: rotateY(2deg);
}
.rotate-x-2 {
  transform: rotateX(2deg);
}

.animate-pulse-fast {
  animation: pulse-fast 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}
.animate-pulse-fast-delay {
  animation: pulse-fast 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
  animation-delay: 1s;
}
@keyframes pulse-fast {
  0%, 100% { opacity: 0.2; transform: scale(1); }
  50% { opacity: 0.4; transform: scale(1.05); }
}

.animate-pulse-slow {
  animation: pulse-slow 8s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}
.animate-pulse-slow-delay {
  animation: pulse-slow 8s cubic-bezier(0.4, 0, 0.6, 1) infinite;
  animation-delay: 4s;
}
@keyframes pulse-slow {
  0%, 100% { opacity: 0.3; transform: scale(1) translateZ(0); }
  50% { opacity: 0.5; transform: scale(1.1) translateZ(0); }
}

@keyframes glare {
  0% { transform: translate(-50%, -50%) rotate(45deg); }
  100% { transform: translate(150%, 150%) rotate(45deg); }
}
.animate-glare {
  animation: glare 1.5s ease-in-out forwards;
}

@keyframes loading-bar {
  0% { transform: translateX(-100%); }
  100% { transform: translateX(100%); }
}
.animate-loading-bar {
  animation: loading-bar 1.5s ease-in-out infinite;
  width: 100%;
}
</style>
