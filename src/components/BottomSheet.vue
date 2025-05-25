<template>
    <transition name="fade">
        <div v-if="modelValue" class="fixed inset-0 z-50 flex items-end justify-center bg-black/50"
            @click="$emit('update:modelValue', false)">
            <div class="bg-white w-full max-w-md rounded-t-2xl shadow-lg p-4 transition-transform duration-300" :class="{
                'translate-y-0': modelValue,
                'translate-y-full': !modelValue
            }" @click.stop="x">
                <!-- Drag Handle -->
                <div class="w-12 h-1.5 bg-gray-300 rounded-full mx-auto mb-4"></div>

                <!-- Optional title -->
                <div v-if="title" class="text-center font-semibold text-lg mb-2">
                    {{ title }}
                </div>

                <!-- Close Button -->
                <button class="absolute top-2 right-4 text-gray-500" @click="$emit('update:modelValue', false)">
                    ✕
                </button>

                <!-- Default slot -->
                <div>
                    <slot />
                </div>
            </div>
        </div>
    </transition>
</template>

<script setup>
defineProps({
    modelValue: Boolean,
    title: String,
});
defineEmits(['update:modelValue']);
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.2s;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}
</style>