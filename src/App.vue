<template>
    <div class="min-h-screen w-full flex flex-col bg-white" :style="{ backgroundImage: `url(${bgUrl})` }">
        <div class="absolute inset-0 bg-white/60"></div>
        <div
            class="relative z-10 h-[40vh] bg-gradient-to-b from-purple-800 to-purple-500 text-white text-center p-6 rounded-b-3xl flex flex-col items-center justify-between">
            <h3 class="font-bold text-xl">POS PERJUANGAN</h3>
            <div class="">
                <p class="mt-">Sisa Saldo</p>
                <h3 class="text-3xl font-bold">{{ data.saldoAkhir }}</h3>
            </div>
            <div class="grid grid-cols-4 w-full">
                <a @click="cashInShow = true" class="flex flex-col items-center justify-center gap-1">
                    <div class="rounded-full w-12 h-12 bg-white/30 text-center flex items-center justify-center">
                        <PhArrowDown :size="24" />
                    </div>
                    <span class="">Masuk</span>
                </a>
                <a @click="cashOutShow = true" class="flex flex-col items-center justify-center gap-1">
                    <div class="rounded-full w-12 h-12 bg-white/30 text-center flex items-center justify-center">
                        <PhArrowUp :size="24" />
                    </div>
                    <span class="">Keluar</span>
                </a>
                <a href="https://docs.google.com/spreadsheets/d/e/2PACX-1vQkQ_-7W2vwqEetmPNpqpRj_CiAllylg0jmGnvHcuylH-qWcktqX58ffDGTPZMeP1RsBpO_7kWPYk7H/pubhtml"
                    class="flex flex-col items-center justify-center gap-1">
                    <div class="rounded-full w-12 h-12 bg-white/30 text-center flex items-center justify-center">
                        <PhArrowsDownUp :size="24" />
                    </div>
                    <span class="">Rincian</span>
                </a>
                <a @click="donateShow = true" class="flex flex-col items-center justify-center gap-1">
                    <div class="rounded-full w-12 h-12 bg-white/30 text-center flex items-center justify-center">
                        <PhHandHeart :size="24" />
                    </div>
                    <span class="">Donasi</span>
                </a>
                <!-- <a href="#" class="flex flex-col items-center justify-center gap-1">
                    <div class="rounded-full w-12 h-12 bg-white/30 text-center flex items-center justify-center">
                        <PhHandHeart :size="24" />
                    </div>
                    <span class="">Donasi</span>
                </a> -->
            </div>
            <!-- <div class="bg-red-300 w-20 h-20 absolute top-[-2]">

            </div> -->

        </div>
        <div class="flex-1 relative z-10">
            <div class="grid grid-cols-2 p-12 gap-6">
                <a href="https://drive.google.com/drive/folders/1u458Rqull3jwymRdbH9fcylNJV5Kygi8?usp=drive_link"
                    class="bg-white rounded-xl h-32 w-full shadow-md flex flex-col items-center justify-center gap-2">
                    <PhImages :size="42" color="oklch(49.6% 0.265 301.924)" />
                    <span class="text-neutral-500 text-center">Galeri</span>
                </a>
                <a href="https://quran.nu.or.id/"
                    class="bg-white rounded-xl h-32 w-full shadow-md flex flex-col items-center justify-center gap-2">
                    <PhBookBookmark :size="42" color="oklch(49.6% 0.265 301.924)" />
                    <span class="text-neutral-500 text-center">Qur'an & Dzikir</span>
                </a>
                <a @click="wifiShow = true"
                    class="bg-white rounded-xl h-32 w-full shadow-md flex flex-col items-center justify-center gap-2">
                    <PhWifiHigh :size="42" color="oklch(49.6% 0.265 301.924)" />
                    <span class="text-neutral-500 text-center">Wi-Fi</span>
                </a>

            </div>
        </div>

        <BottomSheet v-model="cashInShow" title="Kas Masuk">
            <p>Adapun total kas masuk adalah: {{ data.pemasukan }}</p>
        </BottomSheet>
        <BottomSheet v-model="cashOutShow" title="Kas Keluar">
            <p>Adapun total kas keluar adalah: {{ data.pengeluaran }}</p>
        </BottomSheet>
        <BottomSheet v-model="donateShow" title="Donasi">
            <p>Jika berkenan donasi hubungi kami di link berikut: </p>
            <div class="text-center w-full flex justify-center mt-3"><a
                    class="px-3 py-1 rounded-lg border bg-green-600 font-semibold text-white" :href="whatsappLink"
                    target="_blank">Hubungi
                    Admin</a></div>
        </BottomSheet>
        <BottomSheet v-model="wifiShow" title="Informasi Wifi">
            <p>SSID : POS TAMAN</p>
            <p>PASSWORD : 123123123</p>
        </BottomSheet>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import BottomSheet from './components/BottomSheet.vue'

const nomor = '6285333920007' // Ganti dengan nomor tujuan
const pesan = 'Assalamualaikum.. '
const whatsappLink = `https://wa.me/${nomor}?text=${encodeURIComponent(pesan)}`

const cashInShow = ref(false)
const cashOutShow = ref(false)
const donateShow = ref(false)
const wifiShow = ref(false)

const bgUrl = '/images/bg.jpg'

const formatRupiah = (value) => {
    return new Intl.NumberFormat('id-ID', {
        style: 'currency',
        currency: 'IDR',
        minimumFractionDigits: 0,
    }).format(value)
}

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