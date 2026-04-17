<template>
  <div class="min-h-screen bg-gradient-to-br from-sky-400 via-blue-500 to-blue-600 flex items-center justify-center p-4 relative overflow-hidden">
    <!-- Clouds -->
    <div class="absolute top-10 left-10 opacity-70">
      <svg width="100" height="60" viewBox="0 0 100 60" fill="white">
        <circle cx="20" cy="40" r="15"/>
        <circle cx="35" cy="35" r="18"/>
        <circle cx="50" cy="40" r="15"/>
        <circle cx="65" cy="38" r="12"/>
      </svg>
    </div>
    <div class="absolute top-20 right-20 opacity-60">
      <svg width="120" height="70" viewBox="0 0 120 70" fill="white">
        <circle cx="25" cy="45" r="18"/>
        <circle cx="45" cy="40" r="22"/>
        <circle cx="65" cy="45" r="18"/>
        <circle cx="85" cy="42" r="15"/>
      </svg>
    </div>
    <div class="absolute bottom-20 left-1/4 opacity-50">
      <svg width="80" height="50" viewBox="0 0 80 50" fill="white">
        <circle cx="15" cy="35" r="12"/>
        <circle cx="30" cy="30" r="15"/>
        <circle cx="45" cy="35" r="12"/>
        <circle cx="60" cy="33" r="10"/>
      </svg>
    </div>
    <!-- Birds -->
    <div class="absolute top-32 left-1/3 opacity-80">
      <svg width="40" height="20" viewBox="0 0 40 20" fill="none" stroke="white" stroke-width="2">
        <path d="M5 10 Q10 5 15 10 Q20 15 25 10 Q30 5 35 10"/>
        <circle cx="8" cy="8" r="1"/>
        <circle cx="12" cy="8" r="1"/>
        <circle cx="28" cy="8" r="1"/>
        <circle cx="32" cy="8" r="1"/>
      </svg>
    </div>
    <div class="absolute top-40 right-1/3 opacity-70">
      <svg width="50" height="25" viewBox="0 0 50 25" fill="none" stroke="white" stroke-width="2">
        <path d="M5 12 Q12 7 20 12 Q28 17 35 12 Q42 7 50 12"/>
        <circle cx="10" cy="10" r="1"/>
        <circle cx="15" cy="10" r="1"/>
        <circle cx="35" cy="10" r="1"/>
        <circle cx="40" cy="10" r="1"/>
      </svg>
    </div>
    <div class="max-w-2xl w-full relative z-10">
      <!-- Header -->
      <div class="text-center mb-12">
        <h1 class="text-5xl font-bold bg-gradient-to-r from-blue-400 to-cyan-400 bg-clip-text text-transparent mb-3">
          QR Code Generator
        </h1>
        <p class="text-gray-400 text-lg">Create beautiful QR codes instantly</p>
      </div>

      <!-- Main Card -->
      <div class="bg-gradient-to-br from-slate-800 to-slate-700 rounded-2xl shadow-2xl p-8 border border-slate-600/50">
        <!-- Text Input -->
        <div class="mb-8">
          <label class="block text-sm font-semibold text-gray-300 mb-3">Text to Encode</label>
          <UInput
            v-model="text"
            placeholder="Enter text or URL..."
            class="w-full"
            size="lg"
          />
        </div>

        <!-- Variant Selector -->
        <div class="mb-8">
          <label class="block text-sm font-semibold text-gray-300 mb-3">QR Style</label>
          <USelect
            v-model="variant"
            :items="variants"
            placeholder="Select a style..."
            class="w-full"
            size="lg"
          />
        </div>

        <!-- QR Code Display -->
        <div class="flex justify-center mb-8">
          <div class="bg-gradient-to-br from-white/10 to-white/5 rounded-xl p-8 border border-white/10 shadow-inner">
            <img
              :src="qr"
              alt="QR Code"
              width="300"
              height="300"
              class="transition-transform duration-300 hover:scale-105"
            />
          </div>
        </div>

        <!-- Info Text -->
        <div class="text-center text-sm text-gray-400">
          <p>{{ text.length }} characters • Scan to test</p>
        </div>
      </div>

      <!-- Footer -->
      <div class="text-center mt-8 text-gray-500 text-sm">
        <p>✨ Powered by Nuxt QR Code</p>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { SVGVariant } from "nuxt-qrcode";

const text = ref("Hello World");
const variant = ref<SVGVariant>("dots");
const variants = ref(["default", "circle", "pixelated", "rounded", "dots"]);

const qr = useQrcode(text, {
  toBase64: true,
  variant: {
    inner: variant.value,
    marker: "rounded",
    pixel: variant.value,
  },
  radius: 1,
  blackColor: "currentColor",
  whiteColor: "#ffffff",
});

watch(variant, () => {
  qr.value = useQrcode(text, {
    toBase64: true,
    variant: {
      inner: variant.value,
      marker: "rounded",
      pixel: variant.value,
    },
    radius: 1,
    blackColor: "currentColor",
    whiteColor: "#ffffff",
  });
});
</script>
