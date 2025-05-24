<template>
  <div class="min-h-screen bg-gray-100 flex flex-col items-center p-6">
    <h1 class="text-3xl font-bold mb-6">POS PERJUANGAN</h1>
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

// Ini URL "echo" final dari GAS yang sudah bebas redirect dan CORS
const URL_GAS =
  'https://script.googleusercontent.com/macros/echo?user_content_key=AehSKLjcYc_5FqxrUrCtXyWwXNR6178mjc3BUHi6khno3bujtdSH6lReBZbHT3_9bm2pvwziz2Q5TaRRVytJL9i1hQCUFGknQ6yljOLwcCRW3BfFevU6dYdHwNLMi18_D-qHIzx20mL143-fAVkamBcIMJxWfE8BXzEb5WWmHTnKusTllv4KBN2Tr6FWYXocT6oWVlTzw7oSLxaC1qLZNceKu9RiHpUsMgpmZgs9H1_jrxsMbOlmvPaviR_ZrKJqFg&lib=M7R5khhdfR7mU81mlfHyO8bee_uHNINZP';

onMounted(async () => {
  loading.value = true;
  error.value = null;
  try {
    const res = await fetch(URL_GAS);
    if (!res.ok) throw new Error(`HTTP error! status: ${res.status}`);
    const json = await res.json();
    data.value = json;
  } catch (e) {
    error.value = e.message;
  } finally {
    loading.value = false;
  }
});
</script>

<style>
/* Tailwind sudah disetup via vite.config.js, pastikan sudah install tailwindcss */
</style>
