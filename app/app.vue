<template>
  <UContainer>
    <UInput v-model="text" />
    <USelect v-model="variant" :items="variants" />

    <img style="margin: 30px;box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;border-radius: 10px;" class="w-full h-full " width="300" :src="qr" alt="QR Code" />
  </UContainer>
</template>

<script setup lang="ts">
import type { SVGVariant } from "nuxt-qrcode";

const text = ref("Hello World");
const variant = ref<SVGVariant>("dots");
const variants = ref(["default", "circle", "pixelated", "rounded", "dots"]);

const qr = useQrcode(text, {
  toBase64: true,
 variant: {
        inner: 'dots',
        marker: 'rounded',
        pixel: 'rounded',
      },
   radius: 1,
  blackColor: "currentColor",
  whiteColor: "#ffff",
});
</script>
