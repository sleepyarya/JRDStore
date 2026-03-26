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
        <a :href="contacts.roblox" target="_blank" class="hover:text-gray-400 transition-colors duration-300"><i class="fas fa-gamepad"></i> Roblox Jhordi</a>
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
              <div v-if="item.isBestSeller" class="absolute top-0 right-0 bg-gradient-to-r from-yellow-400 to-yellow-600 text-black text-xs font-black px-3 py-1 rounded-bl-xl shadow-lg z-10 font-racing tracking-wider transform translate-x-[1px] -translate-y-[1px]">
                BEST SELLER
              </div>
              <div class="absolute inset-0 bg-gradient-to-br from-jrd-purple/20 to-transparent opacity-0 group-hover:opacity-100 transition-opacity"></div>
              <div class="p-6 text-center transform transition-transform group-hover:scale-105">
                <div class="text-jrd-light-purple font-racing text-3xl font-bold mb-2 drop-shadow-lg">{{ item.amount }} R$</div>
                <div class="text-gray-300 font-bold text-lg">IDR {{ item.price }}</div>
                <button @click="openModal(item.amount + ' R$ - IDR ' + item.price)" class="block text-center mt-4 w-full py-2 bg-white/10 hover:bg-jrd-purple hover:text-white rounded text-sm font-bold uppercase tracking-wide transition-colors cursor-pointer">
                  Beli
                </button>
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
                 
                 <button @click="openModal(item.name + ' - IDR ' + item.priceIdr)" class="block mt-4 w-full text-center py-3 bg-jrd-purple text-white font-black font-racing uppercase rounded hover:bg-purple-500 transition-colors shadow-lg shadow-purple-900/20 cursor-pointer">
                   ORDER NOW
                 </button>
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
                 
                 <button @click="openModal(item.name + ' - IDR ' + item.priceIdr)" class="block mt-4 w-full text-center py-3 bg-jrd-purple text-white font-black font-racing uppercase rounded hover:bg-purple-500 transition-colors shadow-lg shadow-purple-900/20 cursor-pointer">
                   ORDER NOW
                 </button>
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

    <!-- ===================== QRIS PAYMENT MODAL ===================== -->
    <Transition name="modal-fade">
      <div v-if="showModal" class="fixed inset-0 z-50 flex items-center justify-center p-4" @click.self="closeModal">
        <!-- Backdrop -->
        <div class="absolute inset-0 bg-black/80 backdrop-blur-md"></div>

        <!-- Modal Box -->
        <div class="relative bg-gradient-to-b from-gray-900 to-black border border-purple-500/30 rounded-2xl shadow-[0_0_60px_rgba(147,51,234,0.4)] w-full max-w-sm overflow-hidden modal-box">
          
          <!-- Purple glow top -->
          <div class="absolute top-0 left-0 right-0 h-1 bg-gradient-to-r from-transparent via-jrd-purple to-transparent"></div>

          <!-- Header -->
          <div class="px-6 pt-6 pb-4 text-center">
            <div class="text-xs font-bold uppercase tracking-widest text-purple-400 mb-1">Pembayaran</div>
            <h2 class="text-xl font-racing font-black text-white">Scan QRIS untuk Bayar</h2>
            <p class="text-gray-400 text-sm mt-1">{{ selectedItem }}</p>
          </div>

          <!-- QRIS Image -->
          <div class="px-6 pb-2 flex justify-center">
            <div class="relative">
              <div class="absolute inset-0 rounded-xl bg-jrd-purple/20 blur-xl scale-110"></div>
              <img src="./assets/qris.png" alt="QRIS Payment" class="relative rounded-xl w-64 h-64 object-cover shadow-2xl border border-purple-500/20 qris-img" />
            </div>
          </div>

          <!-- Info -->
          <div class="px-6 py-3 text-center">
            <p class="text-gray-400 text-xs">Scan QR di atas menggunakan aplikasi dompet digital kamu</p>
          </div>

          <!-- Divider -->
          <div class="mx-6 border-t border-white/10 my-2"></div>

          <!-- Action Buttons -->
          <div class="px-6 pb-6 flex flex-col gap-3 mt-2">
            <!-- Sudah Bayar Button -->
            <button @click="confirmPayment" class="w-full py-3 bg-gradient-to-r from-green-600 to-emerald-500 hover:from-green-500 hover:to-emerald-400 text-white font-black font-racing uppercase rounded-xl transition-all duration-300 shadow-lg shadow-green-900/30 tracking-wider hover:scale-[1.02] active:scale-95">
              <i class="fas fa-check-circle mr-2"></i> Sudah Bayar
            </button>

            <!-- Chat TikTok Button -->
            <a :href="contacts.tiktok" target="_blank" class="w-full py-3 flex items-center justify-center gap-2 bg-gradient-to-r from-[#010101] to-[#1a1a2e] border border-white/10 hover:border-purple-500/50 text-white font-black font-racing uppercase rounded-xl transition-all duration-300 hover:scale-[1.02] active:scale-95">
              <i class="fab fa-tiktok text-white"></i>
              <span>Chat TikTok</span>
            </a>

            <!-- Tutup -->
            <button @click="closeModal" class="w-full py-2 text-gray-500 hover:text-white text-sm font-bold uppercase tracking-wider transition-colors duration-200">
              Tutup
            </button>
          </div>
        </div>
      </div>
    </Transition>

  </div>
</template>

<script setup>
import { ref } from 'vue'
import { robuxList, gamepassList, moneyList, contacts } from './data.js'
import LoadingScreen from './components/LoadingScreen.vue'

const filter = ref('all')
const showModal = ref(false)
const selectedItem = ref('')

function openModal(itemLabel) {
  selectedItem.value = itemLabel
  showModal.value = true
  document.body.style.overflow = 'hidden'
}

function closeModal() {
  showModal.value = false
  document.body.style.overflow = ''
}

function confirmPayment() {
  closeModal()
  window.open(contacts.tiktok, '_blank')
}
</script>

<style>
/* Custom animations if needed */

/* ===== Modal Transition ===== */
.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: opacity 0.3s ease;
}
.modal-fade-enter-active .modal-box,
.modal-fade-leave-active .modal-box {
  transition: transform 0.35s cubic-bezier(0.34, 1.56, 0.64, 1), opacity 0.3s ease;
}
.modal-fade-enter-from,
.modal-fade-leave-to {
  opacity: 0;
}
.modal-fade-enter-from .modal-box {
  transform: scale(0.8) translateY(30px);
  opacity: 0;
}
.modal-fade-leave-to .modal-box {
  transform: scale(0.9) translateY(20px);
  opacity: 0;
}

/* QRIS pulse animation */
.qris-img {
  animation: qris-pulse 2.5s ease-in-out infinite;
}
@keyframes qris-pulse {
  0%, 100% { box-shadow: 0 0 0 0 rgba(147, 51, 234, 0.4); }
  50% { box-shadow: 0 0 0 12px rgba(147, 51, 234, 0); }
}

/* ===== Success Animation ===== */
.success-fade-enter-active,
.success-fade-leave-active {
  transition: opacity 0.4s ease;
}
.success-fade-enter-from,
.success-fade-leave-to {
  opacity: 0;
}

.success-popup {
  animation: popup-bounce 0.5s cubic-bezier(0.34, 1.56, 0.64, 1);
}
@keyframes popup-bounce {
  from { transform: scale(0.5); opacity: 0; }
  to   { transform: scale(1);   opacity: 1; }
}

.success-circle {
  width: 100px;
  height: 100px;
  background: radial-gradient(circle, rgba(16,185,129,0.3), transparent 70%);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  filter: drop-shadow(0 0 24px rgba(16, 185, 129, 0.8));
}

.checkmark {
  width: 80px;
  height: 80px;
}

.checkmark-circle {
  stroke: #10b981;
  stroke-width: 2;
  stroke-dasharray: 166;
  stroke-dashoffset: 166;
  animation: stroke 0.6s cubic-bezier(0.65, 0, 0.45, 1) forwards;
}

.checkmark-check {
  stroke: #10b981;
  stroke-width: 3;
  stroke-linecap: round;
  stroke-linejoin: round;
  stroke-dasharray: 48;
  stroke-dashoffset: 48;
  animation: stroke 0.3s cubic-bezier(0.65, 0, 0.45, 1) 0.5s forwards;
}

@keyframes stroke {
  100% { stroke-dashoffset: 0; }
}

.success-text {
  animation: fade-up 0.5s ease 0.4s both;
}
.success-subtext {
  animation: fade-up 0.5s ease 0.6s both;
}
@keyframes fade-up {
  from { opacity: 0; transform: translateY(10px); }
  to   { opacity: 1; transform: translateY(0); }
}
</style>
