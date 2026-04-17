<template>
  <div class="min-h-screen bg-gradient-to-br from-slate-900 via-slate-800 to-slate-900 flex items-center justify-center p-4">
    <div class="max-w-2xl w-full">
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
