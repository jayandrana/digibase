<template>
  <div class="min-h-screen bg-slate-50 text-slate-800 antialiased">
    <header class="sticky top-0 z-30 border-b border-slate-200/80 bg-white/80 backdrop-blur-xl">
      <div class="mx-auto flex max-w-7xl items-center justify-between px-6 py-4 lg:px-8">
        <div class="flex items-center gap-3">
          <div class="flex h-11 w-11 items-center justify-center rounded-2xl bg-indigo-600 text-lg font-bold text-white shadow-[0_12px_40px_rgba(79,70,229,0.18)]">
            DE
          </div>
          <div>
            <h1 class="text-lg font-bold text-slate-900">Direktori Ekonomi Digital</h1>
            
          </div>
        </div>

        <nav class="hidden items-center gap-8 md:flex">
          <a href="#" class="text-sm font-medium text-slate-600 transition hover:text-indigo-700">Beranda</a>
          <a href="#" class="text-sm font-medium text-slate-600 transition hover:text-indigo-700">Direktori</a>
          <a href="#" class="text-sm font-medium text-slate-600 transition hover:text-indigo-700">Kategori</a>
          <a href="#" class="text-sm font-medium text-slate-600 transition hover:text-indigo-700">Peta</a>
          <a href="#" class="text-sm font-medium text-slate-600 transition hover:text-indigo-700">Tentang</a>
        </nav>

        <div class="flex items-center gap-3">
          <button class="hidden rounded-xl border border-slate-200 px-4 py-2 text-sm font-semibold text-slate-700 transition hover:border-indigo-200 hover:bg-indigo-50 sm:inline-flex">
            Masuk
          </button>
          <button class="rounded-xl bg-indigo-600 px-4 py-2 text-sm font-semibold text-white shadow-[0_12px_40px_rgba(79,70,229,0.18)] transition hover:bg-indigo-700">
            Tambah Data
          </button>
        </div>
      </div>
    </header>
    <section class="relative overflow-hidden">
      <div class="absolute inset-0 bg-gradient-to-br from-indigo-50 via-white to-slate-100"></div>
      <div class="absolute -left-24 top-10 h-72 w-72 rounded-full bg-indigo-200/40 blur-3xl"></div>
      <div class="absolute right-0 top-0 h-80 w-80 rounded-full bg-sky-200/40 blur-3xl"></div>

      <div class="relative mx-auto grid max-w-7xl gap-10 px-6 py-16 lg:grid-cols-[1.2fr_0.8fr] lg:px-8 lg:py-20">
        <div class="self-center">
          <span class="inline-flex rounded-full border border-indigo-200 bg-white px-4 py-1 text-sm font-medium text-indigo-700 shadow-sm">
             Direktori usaha digital SE 2026 Provinsi Bali
          </span>
          
          <p class="mt-5 max-w-2xl text-lg leading-8 text-slate-600">
            UMKM digital, marketplace, fintech, edutech, agrotech, kreator, hingga layanan teknologi di berbagai wilayah di Provinsi Bali.
          </p>

          <div class="mt-8 rounded-3xl border border-white/70 bg-white/90 p-4 shadow-[0_10px_30px_rgba(15,23,42,0.08)] backdrop-blur">
            <div class="grid gap-3 lg:grid-cols-[1.4fr_1fr_1fr_auto]">
              <div>
                <label class="mb-2 block text-sm font-semibold text-slate-600">Cari usaha atau layanan</label>
                <input
                  v-model="filters.keyword"
                  type="text"
                  placeholder="Contoh: startup pendidikan, toko online, software house"
                  class="w-full rounded-2xl border border-slate-200 bg-slate-50 px-4 py-3 text-sm outline-none transition focus:border-indigo-400 focus:bg-white"
                />
              </div>
              <div>
                <label class="mb-2 block text-sm font-semibold text-slate-600">Kategori</label>
                <select v-model="filters.category" class="w-full rounded-2xl border border-slate-200 bg-slate-50 px-4 py-3 text-sm outline-none transition focus:border-indigo-400 focus:bg-white">
                  <option value="">Semua kategori</option>
                  <option v-for="category in categories" :key="category" :value="category">{{ category }}</option>
                </select>
              </div>
              <div>
                <label class="mb-2 block text-sm font-semibold text-slate-600">Wilayah</label>
                <select v-model="filters.region" class="w-full rounded-2xl border border-slate-200 bg-slate-50 px-4 py-3 text-sm outline-none transition focus:border-indigo-400 focus:bg-white">
                  <option value="">Semua wilayah</option>
                  <option v-for="region in regions" :key="region" :value="region">{{ region }}</option>
                </select>
              </div>
              <div class="flex items-end">
                <button @click="resetFilters" class="w-full rounded-2xl bg-indigo-600 px-5 py-3 text-sm font-semibold text-white transition hover:bg-indigo-700">
                  Reset
                </button>
              </div>
            </div>
          </div>

          <div class="mt-8 grid max-w-2xl grid-cols-2 gap-4 md:grid-cols-4">
            <div class="rounded-2xl border border-slate-200 bg-white/90 p-4 shadow-sm">
              <div class="text-2xl font-bold text-slate-900">1500+</div>
              <div class="mt-1 text-sm text-slate-500">Usaha terdaftar</div>
            </div>
            <div class="rounded-2xl border border-slate-200 bg-white/90 p-4 shadow-sm">
              <div class="text-2xl font-bold text-slate-900">{{ categories.length }}</div>
              <div class="mt-1 text-sm text-slate-500">Kategori</div>
            </div>
            <div class="rounded-2xl border border-slate-200 bg-white/90 p-4 shadow-sm">
              <div class="text-2xl font-bold text-slate-900">{{ regions.length }}</div>
              <div class="mt-1 text-sm text-slate-500">Wilayah</div>
            </div>
            <div class="rounded-2xl border border-slate-200 bg-white/90 p-4 shadow-sm">
              <div class="text-2xl font-bold text-slate-900">24/7</div>
              <div class="mt-1 text-sm text-slate-500">Akses publik</div>
            </div>
          </div>
        </div>

        <div class="relative">
          <div class="rounded-[2rem] border border-white/80 bg-white/90 p-5 shadow-[0_10px_30px_rgba(15,23,42,0.08)] backdrop-blur">
            <div class="rounded-[1.5rem] bg-slate-900 p-5 text-white">
              <div class="flex items-center justify-between">
                <div>
                  <p class="text-sm text-slate-400">Insight Ringkas</p>
                  <h3 class="mt-1 text-xl font-semibold">Sebaran Ekonomi Digital</h3>
                </div>
                <div class="rounded-2xl bg-white/10 px-3 py-1 text-sm">2026</div>
              </div>

             
            </div>

            <div class="mt-5 grid gap-4 sm:grid-cols-2">
              <div class="rounded-2xl border border-slate-200 p-4">
                <p class="text-sm text-slate-500">Pertumbuhan data</p>
                <p class="mt-2 text-3xl font-bold text-slate-900">+18.4%</p>
                <p class="mt-1 text-sm text-emerald-600">dibanding semester lalu</p>
              </div>
              <div class="rounded-2xl border border-slate-200 p-4">
                <p class="text-sm text-slate-500">Usaha tervalidasi</p>
                <p class="mt-2 text-3xl font-bold text-slate-900">87%</p>
                <p class="mt-1 text-sm text-slate-500">siap tampil untuk publik</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
     <section class="mx-auto max-w-7xl px-6 pb-6 lg:px-8">
      <div class="rounded-3xl border border-slate-200 bg-white p-5 shadow-[0_10px_30px_rgba(15,23,42,0.08)]">
        <div class="flex flex-col gap-4 lg:flex-row lg:items-center lg:justify-between">
          <div>
            <h3 class="text-lg font-semibold text-slate-900">Direktori Utama</h3>
              </div>

          <div class="flex flex-wrap gap-3">
            
            <label><input type="checkbox" v-model="filters2.instagram"/> Instagram</label> 
            <label><input type="checkbox" v-model="filters2.website"/> Website</label> 
            <label><input type="checkbox" v-model="filters2.linkedin"/> LinkedIn</label> 
            <label><input type="checkbox" v-model="filters2.youtube"/> Youtube</label> 


          </div>
        </div>
      </div>
    </section>


<main class="mx-auto max-w-7xl px-6 pb-16 lg:px-8">
  <div>
    

    <!-- Loading indicator -->
    <div v-if="loading">Loading data...</div>

    <!-- Error message -->
    <div v-else-if="error">{{ error }}</div>

    <!-- Data list -->
    <div v-else>
      <div v-for="item in filteredItems" :key="item.id" class="card">
        <h3>{{ item.nama_usaha }}</h3>
          <p>
          <a 
            :href="`https://www.google.com/maps?q=${item.latitude},${item.longitude}`" 
            target="_blank" 
            rel="noopener noreferrer"
          >
            {{ item.alamat }}
          </a>
        </p>
        <span>{{ item.kabupaten }} - {{ item.subsektor }}</span>

        <!-- Instagram -->
        <div v-if="item.instagram && item.instagram.length > 1">
          <a :href="`${item.instagram}`" target="_blank" rel="noopener noreferrer">
            <i class="fab fa-instagram"></i> {{ item.instagram }}
          </a>
        </div>
          
        <div v-if="item.website && item.website.length > 1">
          <a :href="`https://${item.website}`" target="_blank" rel="noopener noreferrer">
            🌐 {{ item.website }}
          </a>
        </div>

                  <!-- WhatsApp -->
                  <div v-if="item.whatsapp && item.whatsapp.length > 1">
                    <a :href="`https://wa.me/${item.whatsapp}`" target="_blank" rel="noopener noreferrer">
                      📱 WhatsApp: {{ item.whatsapp }}
                    </a>
                  </div>

                  <!-- Email -->
                  <div v-if="item.email && item.email.length > 1">
                    <a :href="`mailto:${item.email}`">
                      ✉️ {{ item.email }}
                    </a>
                  </div>

                  <!-- Shopee -->
                  <div v-if="item.shopee && item.shopee.length > 1">
                    <a :href="item.shopee" target="_blank" rel="noopener noreferrer">
                      🛒 Shopee : {{ item.shopee }}
                    </a>
                  </div>

                  <!-- LinkedIn -->
                  <div v-if="item.linkedin && item.linkedin.length > 1">
                    <a :href="item.linkedin" target="_blank" rel="noopener noreferrer">
                  💼 LinkedIn : {{ item.linkedin }}
                    </a>
                  </div>

                  <!-- YouTube -->
                  <div v-if="item.youtube && item.youtube.length > 1">
                    <a :href="item.youtube" target="_blank" rel="noopener noreferrer">
                      ▶️ YouTube : {{ item.youtube }}
                    </a>
                  </div>
                   <!-- Sumber -->
                  <div v-if="item.sumber && item.sumber.length > 1">
                    <a :href="item.sumber" target="_blank" rel="noopener noreferrer">
                      📚 Sumber : {{ item.sumber }}
                    </a>
                  </div>
            </div>

            <!-- Debug: show raw JSON 
            <pre>{{ directoryItems1 }}</pre>-->
          </div>
        </div>
        </main>
        </div>

</template>

<script setup>
import { ref, onMounted , computed, reactive} from 'vue'
import axios from 'axios'

const directoryItems1 = ref([])
const loading = ref(true)
const error = ref(null)

onMounted(async () => {
  try {
    const apiUrl = 'https://digidbase.statsbali.id/api/products'
    const response = await axios.get(apiUrl)

    // Simulate delay before setting data
    setTimeout(() => {
      directoryItems1.value = response.data
      console.log('Loaded items:', directoryItems1.value)
      loading.value = false
    }, 1000)
  } catch (err) {
    error.value = 'Failed to load data'
    loading.value = false
    console.error(err)
  }
})
const filters2 = ref({
  instagram: false,
  website: false,
  linkedin: false,
  youtube: false
})
const filteredItems = computed(() => {
  
  return directoryItems1.value.filter((item) => {
        // If Instagram filter is checked, require instagram length > 1
    if (filters2.value.instagram && (item.instagram.length <= 1)) {
      return false
    }
    // If Website filter is checked, require website length > 1
    if (filters2.value.website && ( item.website.length <= 1)) {
      return false
    }
    // If LinkedIn filter is checked, require linkedin length > 1
    if (filters2.linkedin && (!item.linkedin || item.linkedin.length <= 1)) {
      return false
    }
    // If YouTube filter is checked, require youtube length > 1
    if (filters2.youtube && (!item.youtube || item.youtube.length <= 1)) {
      return false
    }
    return true

    })
  }
)

//STATIC VARIABEL, CONST
const categories = [
  'Marketplace',
  'Fintech',
  'Edutech',
  'Software House',
  'Kreatif Digital',
  'Agrotech',
  'Marketplace SaaS'
]

const regions = ['Denpasar', 'Badung', 'Gianyar', 'Tabanan']
const quickTabs = ['Startup', 'UMKM Digital', 'Instagram', 'Kreator']
const businessModels = ['B2B', 'B2C', 'Marketplace', 'Subscription']

const activeTab = ref('Semua')
const sortBy = ref('newest')

const filters = ref({
  keyword: '',
  category: '',
  region: '',
  status: '',
  businessModels: []
})

const distributionData = [
  { label: 'Marketplace & E-Commerce', value: 38, barClass: 'bg-indigo-400' },
  { label: 'Jasa Teknologi', value: 27, barClass: 'bg-sky-400' },
  { label: 'Edutech & Konten', value: 19, barClass: 'bg-emerald-400' },
  { label: 'Fintech', value: 16, barClass: 'bg-amber-400' }
]

</script>

<style scoped>
.card {
  border: 1px solid #ddd;
  padding: 12px;
  margin-bottom: 8px;
  border-radius: 4px;
}
</style>
