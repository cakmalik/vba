<template>
  <div class="p-6 max-w-md mx-auto bg-white rounded shadow">
    <h1 class="text-2xl font-bold mb-4">POS PERJUANGAN</h1>
    <div class="space-y-2">
      <div><strong>Pemasukan:</strong> {{ data.pemasukan }}</div>
      <div><strong>Pengeluaran:</strong> {{ data.pengeluaran }}</div>
      <div><strong>Saldo Akhir:</strong> {{ data.saldoAkhir }}</div>
    </div>
    <div v-if="error" class="mt-4 text-red-600">Error: {{ error }}</div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const data = ref({
  pemasukan: '-',
  pengeluaran: '-',
  saldoAkhir: '-'
})
const error = ref(null)

const fetchData = async () => {
  try {
    const res = await fetch('https://script.google.com/macros/s/AKfycbwo2KInJowRLTzYnMuRlLhplGdhLdjJDymsMe4FfLs/dev')
    if (!res.ok) throw new Error(`HTTP error! status: ${res.status}`)
    const json = await res.json()
    data.value = json
    error.value = null
  } catch (err) {
    error.value = err.message
  }
}

onMounted(() => {
  fetchData()
})
</script>
