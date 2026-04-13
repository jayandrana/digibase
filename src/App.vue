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
            <p class="text-sm text-slate-500">Temukan usaha, startup, dan layanan digital dengan lebih mudah</p>
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
          <h2 class="mt-6 max-w-3xl text-4xl font-bold leading-tight text-slate-900 md:text-5xl">
            Jelajahi pelaku <span class="text-indigo-600">ekonomi digital</span> dengan tampilan yang bersih, cepat, dan nyaman.
          </h2>
          <p class="mt-5 max-w-2xl text-lg leading-8 text-slate-600">
            Cocok untuk menampilkan UMKM digital, startup, marketplace, fintech, edutech, agrotech, kreator, hingga layanan teknologi di berbagai wilayah.
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
              <div class="text-2xl font-bold text-slate-900">{{ directoryItems.length }}+</div>
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

              <div class="mt-6 space-y-4">
                <div v-for="item in distributionData" :key="item.label">
                  <div class="mb-2 flex items-center justify-between text-sm">
                    <span class="text-slate-300">{{ item.label }}</span>
                    <span class="font-semibold">{{ item.value }}%</span>
                  </div>
                  <div class="h-3 rounded-full bg-white/10">
                    <div class="h-3 rounded-full" :class="item.barClass" :style="{ width: `${item.value}%` }"></div>
                  </div>
                </div>
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
            <p class="text-sm text-slate-500">Tampilan kartu yang rapi untuk penelusuran cepat dan nyaman.</p>
          </div>

          <div class="flex flex-wrap gap-3">
            <button
              @click="activeTab = 'Semua'"
              :class="activeTab === 'Semua' ? 'bg-indigo-600 text-white' : 'border border-slate-200 text-slate-600 hover:bg-slate-50'"
              class="rounded-full px-4 py-2 text-sm font-semibold"
            >
              Semua
            </button>
            <button
              v-for="tab in quickTabs"
              :key="tab"
              @click="activeTab = tab"
              :class="activeTab === tab ? 'bg-indigo-600 text-white' : 'border border-slate-200 text-slate-600 hover:bg-slate-50'"
              class="rounded-full px-4 py-2 text-sm font-medium"
            >
              {{ tab }}
            </button>
          </div>
        </div>
      </div>
    </section>

    <main class="mx-auto max-w-7xl px-6 pb-16 lg:px-8">
      <div class="grid gap-6 lg:grid-cols-[280px_1fr]">
        <aside class="space-y-5">
          <div class="rounded-3xl border border-slate-200 bg-white p-5 shadow-[0_10px_30px_rgba(15,23,42,0.08)]">
            <h4 class="text-base font-semibold text-slate-900">Filter Tambahan</h4>
            <div class="mt-4 space-y-4">
              <div>
                <label class="mb-2 block text-sm font-medium text-slate-600">Status verifikasi</label>
                <select v-model="filters.status" class="w-full rounded-2xl border border-slate-200 bg-slate-50 px-4 py-3 text-sm outline-none focus:border-indigo-400">
                  <option value="">Semua status</option>
                  <option value="Terverifikasi">Terverifikasi</option>
                  <option value="Proses Validasi">Proses Validasi</option>
                  <option value="Baru">Baru</option>
                </select>
              </div>
              <div>
                <label class="mb-2 block text-sm font-medium text-slate-600">Model bisnis</label>
                <div class="space-y-2 text-sm text-slate-600">
                  <label v-for="business in businessModels" :key="business" class="flex items-center gap-2">
                    <input v-model="filters.businessModels" :value="business" type="checkbox" class="rounded border-slate-300" />
                    {{ business }}
                  </label>
                </div>
              </div>
              <button @click="resetFilters" class="w-full rounded-2xl bg-slate-900 px-4 py-3 text-sm font-semibold text-white transition hover:bg-slate-800">
                Reset Filter
              </button>
            </div>
          </div>

          <div class="rounded-3xl bg-gradient-to-br from-indigo-600 to-indigo-800 p-5 text-white shadow-[0_12px_40px_rgba(79,70,229,0.18)]">
            <p class="text-sm text-indigo-100">Butuh dashboard admin?</p>
            <h4 class="mt-2 text-xl font-semibold">Kelola data usaha digital dengan satu panel terpusat.</h4>
            <p class="mt-3 text-sm leading-6 text-indigo-100">Tambahkan modul validasi, statistik, peta, dan ekspor data untuk kebutuhan instansi atau organisasi.</p>
            <button class="mt-4 rounded-2xl bg-white px-4 py-3 text-sm font-semibold text-indigo-700">
              Lihat Demo Admin
            </button>
          </div>
        </aside>

        <section>
          <div class="mb-5 flex flex-col gap-3 sm:flex-row sm:items-center sm:justify-between">
            <p class="text-sm text-slate-500">Menampilkan {{ filteredItems.length }} entri</p>
            <select v-model="sortBy" class="rounded-2xl border border-slate-200 bg-white px-4 py-3 text-sm text-slate-600 outline-none focus:border-indigo-400">
              <option value="newest">Urutkan: Terbaru</option>
              <option value="name">Urutkan: Nama A-Z</option>
              <option value="region">Urutkan: Wilayah</option>
              <option value="category">Urutkan: Kategori</option>
            </select>
          </div>

          <div class="grid gap-5 md:grid-cols-2 xl:grid-cols-3">
            <article
              v-for="item in sortedItems"
              :key="item.id"
              class="group rounded-3xl border border-slate-200 bg-white p-5 shadow-[0_10px_30px_rgba(15,23,42,0.08)] transition duration-300 hover:-translate-y-1 hover:border-indigo-200 hover:shadow-[0_12px_40px_rgba(79,70,229,0.18)]"
            >
              <div class="flex items-start justify-between gap-3">
                <div :class="item.logoClass" class="flex h-14 w-14 items-center justify-center rounded-2xl text-lg font-bold">
                  {{ item.initial }}
                </div>
                <span :class="statusClass(item.status)" class="rounded-full px-3 py-1 text-xs font-semibold">
                  {{ item.status }}
                </span>
              </div>
              <h3 class="mt-4 text-lg font-bold text-slate-900">{{ item.name }}</h3>
              <p class="mt-1 text-sm text-slate-500">{{ item.category }} · {{ item.region }}</p>
              <p class="mt-4 text-sm leading-6 text-slate-600">{{ item.description }}</p>
              <div class="mt-4 flex flex-wrap gap-2">
                <span v-for="tag in item.tags" :key="tag" class="rounded-full bg-slate-100 px-3 py-1 text-xs text-slate-600">
                  {{ tag }}
                </span>
              </div>
              <div class="mt-5 flex items-center justify-between border-t border-slate-100 pt-4">
                <span class="text-sm font-medium text-slate-500">{{ item.website }}</span>
                <a :href="item.link" class="text-sm font-semibold text-indigo-700">Detail →</a>
              </div>
            </article>
          </div>
        </section>
      </div>
    </main>

    <footer class="border-t border-slate-200 bg-white">
      <div class="mx-auto flex max-w-7xl flex-col gap-4 px-6 py-8 text-sm text-slate-500 lg:flex-row lg:items-center lg:justify-between lg:px-8">
        <p>© 2026 Direktori Ekonomi Digital. Dirancang dengan tampilan modern dan ramah pengguna.</p>
        <div class="flex flex-wrap gap-5">
          <a href="#" class="hover:text-indigo-700">Kebijakan Privasi</a>
          <a href="#" class="hover:text-indigo-700">Syarat Layanan</a>
          <a href="#" class="hover:text-indigo-700">Kontak</a>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { computed, ref,onMounted  } from 'vue'
import axios from 'axios';

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
const quickTabs = ['Startup', 'UMKM Digital', 'Fintech', 'Kreator']
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
onMounted(() => {
  // Simulasi pengambilan data dari API
  const apiUrl = 'http://localhost:3000/api/products'
  const response =  axios.get(apiUrl)
  setTimeout(() => {
    directoryItems1.value = response.data
    console.log(directoryItems1.value)

  }, 1000)
})

const directoryItems = [
  {
    id: 1,
    initial: 'ED',
    name: 'EduSmart Nusantara',
    category: 'Edutech',
    region: 'Denpasar',
    status: 'Terverifikasi',
    description: 'Platform pembelajaran digital yang menyediakan kelas, evaluasi online, dan dashboard analitik untuk siswa dan pengajar.',
    tags: ['LMS', 'Analytics', 'B2B'],
    website: 'www.edusmart.id',
    link: '#',
    type: 'Startup',
    logoClass: 'bg-indigo-100 text-indigo-700'
  },
  {
    id: 2,
    initial: 'FP',
    name: 'FinPay Bali',
    category: 'Fintech',
    region: 'Badung',
    status: 'Terverifikasi',
    description: 'Layanan pembayaran digital untuk UMKM, integrasi QRIS, dashboard transaksi, dan pelaporan penjualan real-time.',
    tags: ['QRIS', 'Payment', 'UMKM'],
    website: 'www.finpaybali.id',
    link: '#',
    type: 'Fintech',
    logoClass: 'bg-sky-100 text-sky-700'
  },
  {
    id: 3,
    initial: 'CH',
    name: 'CreativeHub Studio',
    category: 'Kreatif Digital',
    region: 'Gianyar',
    status: 'Proses Validasi',
    description: 'Studio kreatif untuk branding, desain konten, manajemen media sosial, dan pengembangan identitas visual bisnis lokal.',
    tags: ['Branding', 'Social Media', 'Design'],
    website: 'www.creativehub.co.id',
    link: '#',
    type: 'Kreator',
    logoClass: 'bg-violet-100 text-violet-700'
  },
  {
    id: 4,
    initial: 'AG',
    name: 'AgroTech Connect',
    category: 'Agrotech',
    region: 'Tabanan',
    status: 'Terverifikasi',
    description: 'Aplikasi penghubung petani, distributor, dan pasar digital untuk mendukung rantai pasok hasil pertanian yang efisien.',
    tags: ['Supply Chain', 'Agriculture', 'B2B'],
    website: 'www.agrotechconnect.id',
    link: '#',
    type: 'Startup',
    logoClass: 'bg-emerald-100 text-emerald-700'
  },
  {
    id: 5,
    initial: 'MS',
    name: 'MarketSync Asia',
    category: 'Marketplace SaaS',
    region: 'Denpasar',
    status: 'Terverifikasi',
    description: 'Solusi pembuatan toko online, integrasi inventori, order management, serta sinkronisasi penjualan lintas kanal digital.',
    tags: ['E-Commerce', 'Inventory', 'SaaS'],
    website: 'www.marketsync.asia',
    link: '#',
    type: 'UMKM Digital',
    logoClass: 'bg-rose-100 text-rose-700'
  },
  {
    id: 6,
    initial: 'SW',
    name: 'Softworks Nusantara',
    category: 'Software House',
    region: 'Denpasar',
    status: 'Baru',
    description: 'Pengembang aplikasi web dan mobile untuk bisnis, lembaga pendidikan, koperasi, dan pemerintahan daerah.',
    tags: ['Web App', 'Mobile App', 'Custom System'],
    website: 'www.softworks.id',
    link: '#',
    type: 'Startup',
    logoClass: 'bg-amber-100 text-amber-700'
  }
]


const filteredItems = computed(() => {
  return directoryItems.filter((item) => {
    const keyword = filters.value.keyword.toLowerCase()
    const matchesKeyword =
      !keyword ||
      item.name.toLowerCase().includes(keyword) ||
      item.description.toLowerCase().includes(keyword) ||
      item.category.toLowerCase().includes(keyword)

    const matchesCategory = !filters.value.category || item.category === filters.value.category
    const matchesRegion = !filters.value.region || item.region === filters.value.region
    const matchesStatus = !filters.value.status || item.status === filters.value.status
    const matchesTab = activeTab.value === 'Semua' || item.type === activeTab.value
    const matchesBusinessModel =
      filters.value.businessModels.length === 0 ||
      filters.value.businessModels.some((model) => item.tags.includes(model) || item.description.includes(model))

    return matchesKeyword && matchesCategory && matchesRegion && matchesStatus && matchesTab && matchesBusinessModel
  })
})

const sortedItems = computed(() => {
  const items = [...filteredItems.value]

  switch (sortBy.value) {
    case 'name':
      return items.sort((a, b) => a.name.localeCompare(b.name))
    case 'region':
      return items.sort((a, b) => a.region.localeCompare(b.region))
    case 'category':
      return items.sort((a, b) => a.category.localeCompare(b.category))
    case 'newest':
    default:
      return items.sort((a, b) => b.id - a.id)
  }
})

const resetFilters = () => {
  filters.value = {
    keyword: '',
    category: '',
    region: '',
    status: '',
    businessModels: []
  }
  activeTab.value = 'Semua'
  sortBy.value = 'newest'
}

const statusClass = (status) => {
  if (status === 'Terverifikasi') return 'bg-emerald-50 text-emerald-700'
  if (status === 'Proses Validasi') return 'bg-amber-50 text-amber-700'
  return 'bg-sky-50 text-sky-700'
}



</script>

<style scoped>

</style>
