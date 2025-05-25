<template>
    <div class="min-h-screen w-full flex flex-col bg-white">
        <div
            class="relative h-[40vh] bg-gradient-to-b from-purple-800 to-purple-500 text-white text-center p-6 rounded-b-3xl flex flex-col items-center justify-between">
            <h3 class="font-bold text-xl">POS PERJUANGAN</h3>
            <div class="">
                <p class="mt-">Sisa Saldo</p>
                <h3 class="text-3xl font-bold">Rp24,000</h3>
            </div>
            <div class="grid grid-cols-2 w-full">
                <a href="#" class="flex flex-col items-center justify-center gap-1">
                    <div class="rounded-full w-12 h-12 bg-white/30 text-center flex items-center justify-center">
                        <PhArrowsDownUp :size="24" />
                    </div>
                    <span class="">Rincian</span>
                </a>
                <a href="#" class="flex flex-col items-center justify-center gap-1">
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
        <div class="flex-1 ">
            <div class="grid grid-cols-2 p-12 gap-6">
                <a href="https://drive.google.com/drive/folders/1u458Rqull3jwymRdbH9fcylNJV5Kygi8?usp=drive_link"
                    class="bg-white rounded-lg h-32 w-full shadow-md flex flex-col items-center justify-center">
                    <PhImages :size="42" color="oklch(49.6% 0.265 301.924)" />
                    <span class="text-neutral-500 text-center">Galeri</span>
                </a>
                <div class="bg-white rounded-lg h-32 w-full shadow-md">

                </div>
            </div>
        </div>

    </div>
</template>

<script setup>
import { PhHorse, PhHeart, PhCube } from "@phosphor-icons/vue";
</script>