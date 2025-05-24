<template>
  <div class="min-h-screen bg-gray-100 flex flex-col items-center p-6">
    <h1 class="text-3xl font-bold mb-6">POS PERJUANGAN</h1>
    <div class="min-h-screen bg-gray-100 p-4">
  <!-- Judul Dashboard -->
  <h1 class="text-2xl font-bold text-center mb-6">Dashboard Kas</h1>

  <!-- Saldo Kas -->
  <div class="bg-white shadow-md rounded-xl p-6 text-center mb-6">
    <h2 class="text-gray-600 text-lg mb-2">Saldo Kas</h2>
    <p class="text-3xl font-bold text-blue-600">Rp 5.000.000</p>
  </div>

  <!-- Grid untuk Pemasukan & Pengeluaran -->
  <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
    <!-- Pemasukan -->
    <div class="bg-white shadow-md rounded-xl p-4">
      <h3 class="text-gray-600 text-base mb-1">Pemasukan</h3>
      <p class="text-green-600 font-bold text-xl">Rp 3.500.000</p>
    </div>

    <!-- Pengeluaran -->
    <div class="bg-white shadow-md rounded-xl p-4">
      <h3 class="text-gray-600 text-base mb-1">Pengeluaran</h3>
      <p class="text-red-600 font-bold text-xl">Rp 1.500.000</p>
    </div>
  </div>
</div>

    <div v-if="loading" class="text-gray-600">Loading...</div>
    <div v-else-if="error" class="text-red-600">Error: {{ error }}</div>
    <div v-else class="space-y-4">
      <div class="bg-white p-4 rounded shadow w-64">
        <h2 class="font-semibold text-lg mb-2">Pemasukan</h2>
        <p class="text-green-600 font-bold text-xl">{{ data.pemasukan }}</p>
      </div>
      <div class="bg-white p-4 rounded shadow w-64">
        <h2 class="font-semibold text-lg mb-2">Pengeluaran</h2>
        <p class="text-red-600 font-bold text-xl">{{ data.pengeluaran }}</p>
      </div>
      <div class="bg-white p-4 rounded shadow w-64">
        <h2 class="font-semibold text-lg mb-2">Saldo Akhir</h2>
        <p class="text-blue-600 font-bold text-xl">{{ data.saldoAkhir }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const data = ref({
  pemasukan: 0,
  pengeluaran: 0,
  saldoAkhir: 0,
});
const loading = ref(true);
const error = ref(null);

// URL gsx2json
const SHEET_URL = 'https://gsx2json.com/api?id=1XZkkTcaq8uQM_YWxFPcEslHjybKITTIMTLv3HRD0mdM&sheet=PERJUANGAN';

onMounted(async () => {
  loading.value = true;
  error.value = null;
  try {
    const res = await fetch(SHEET_URL);
    if (!res.ok) throw new Error(`HTTP error! status: ${res.status}`);
    const json = await res.json();

    const arr = json.columns["undefined"];
    const getValueAfterLabel = (label) => {
      const index = arr.indexOf(label);
      return index !== -1 && arr[index + 1] ? arr[index + 1] : 0;
    };

    data.value = {
      pemasukan: getValueAfterLabel("PEMASUKAN"),
      pengeluaran: getValueAfterLabel("PENGELUARAN"),
      saldoAkhir: getValueAfterLabel("SALDO AKHIR"),
    };
  } catch (e) {
    error.value = e.message;
  } finally {
    loading.value = false;
  }
});
</script>
