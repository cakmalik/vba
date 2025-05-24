<template>
  <div class="min-h-screen bg-gray-100 flex flex-col items-center p-6">
    <h1 class="text-3xl font-bold mb-8 text-center text-indigo-700">POS PERJUANGAN</h1>

    <div v-if="loading" class="text-center text-gray-600">Loading data...</div>
    <div v-else-if="error" class="text-center text-red-600">Error: {{ error }}</div>
    <div v-else class="w-full max-w-md bg-white rounded-lg shadow-md p-6 space-y-6">
      <div class="p-4 bg-green-100 rounded shadow">
        <h2 class="text-xl font-semibold text-green-700 mb-2">Pemasukan</h2>
        <p class="text-2xl font-bold text-green-900">{{ data.pemasukan }}</p>
      </div>
      <div class="p-4 bg-red-100 rounded shadow">
        <h2 class="text-xl font-semibold text-red-700 mb-2">Pengeluaran</h2>
        <p class="text-2xl font-bold text-red-900">{{ data.pengeluaran }}</p>
      </div>
      <div class="p-4 bg-blue-100 rounded shadow">
        <h2 class="text-xl font-semibold text-blue-700 mb-2">Saldo Akhir</h2>
        <p class="text-2xl font-bold text-blue-900">{{ data.saldoAkhir }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const data = ref(null)
const error = ref(null)
const loading = ref(true)

const API_URL = 'https://script.google.com/macros/s/AKfycbwZnUW9Bw63i4cAySHn8n5QVhCavUo7EbWTYv1qNYWCMiBeEk74fl4ALgahq_0CLxID/exec'

onMounted(async () => {
  try {
    const res = await fetch(API_URL)
    if (!res.ok) throw new Error('Gagal fetch data')
    const json = await res.json()
    data.value = json
  } catch (err) {
    error.value = err.message
  } finally {
    loading.value = false
  }
})
</script>

<style>
/* optional custom styles */
</style>
