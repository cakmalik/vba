<template>
  <div class="max-w-md mx-auto p-6 bg-white rounded shadow mt-10">
    <h1 class="text-2xl font-bold mb-6 text-center">POS PERJUANGAN</h1>
    
    <div v-if="error" class="text-red-600 font-semibold mb-4">{{ error }}</div>
    
    <div v-if="loading" class="text-gray-500 text-center">Loading...</div>
    
    <div v-if="data && !loading" class="space-y-4">
      <div class="flex justify-between">
        <span class="font-semibold">Pemasukan:</span>
        <span>Rp {{ formatNumber(data.pemasukan) }}</span>
      </div>
      <div class="flex justify-between">
        <span class="font-semibold">Pengeluaran:</span>
        <span>Rp {{ formatNumber(data.pengeluaran) }}</span>
      </div>
      <div class="flex justify-between">
        <span class="font-semibold">Saldo Akhir:</span>
        <span>Rp {{ formatNumber(data.saldoAkhir) }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const data = ref(null)
const loading = ref(true)
const error = ref(null)

// Fungsi JSONP sederhana
function jsonp(url, callbackName = 'callback') {
  return new Promise((resolve, reject) => {
    const script = document.createElement('script')
    window[callbackName] = (data) => {
      resolve(data)
      document.body.removeChild(script)
      delete window[callbackName]
    }
    script.src = `${url}?callback=${callbackName}`
    script.onerror = () => {
      reject(new Error('JSONP request failed'))
      document.body.removeChild(script)
      delete window[callbackName]
    }
    document.body.appendChild(script)
  })
}

function formatNumber(num) {
  if (typeof num !== 'number') return num
  return num.toLocaleString('id-ID')
}

onMounted(async () => {
  const url = 'https://script.google.com/macros/s/AKfycbwZnUW9Bw63i4cAySHn8n5QVhCavUo7EbWTYv1qNYWCMiBeEk74fl4ALgahq_0CLxID/exec'

  try {
    loading.value = true
    const result = await jsonp(url, 'handleResponse')
    if (result.error) {
      error.value = result.error
    } else {
      data.value = result
    }
  } catch (err) {
    error.value = err.message || 'Error fetching data'
  } finally {
    loading.value = false
  }
})
</script>

<style>
/* Tailwind sudah otomatis jika sudah di-setup */
</style>
