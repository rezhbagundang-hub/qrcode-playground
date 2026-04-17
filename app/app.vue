<template>
  <div class="min-h-screen bg-gradient-to-br from-sky-400 via-sky-500 to-blue-700 overflow-hidden">
    <div class="absolute inset-0 bg-[radial-gradient(circle_at_top,_rgba(255,255,255,0.45),_transparent_18%),radial-gradient(circle_at_bottom_right,_rgba(59,130,246,0.18),_transparent_22%)]" />
    <div class="absolute inset-0 pointer-events-none">
      <div class="absolute top-8 left-12 opacity-90">
        <svg width="160" height="100" viewBox="0 0 160 100" fill="white">
          <ellipse cx="46" cy="55" rx="28" ry="22" />
          <ellipse cx="70" cy="45" rx="38" ry="28" />
          <ellipse cx="105" cy="55" rx="26" ry="20" />
          <ellipse cx="130" cy="50" rx="20" ry="16" />
        </svg>
      </div>
      <div class="absolute top-24 right-14 opacity-75">
        <svg width="200" height="110" viewBox="0 0 200 110" fill="white">
          <ellipse cx="52" cy="58" rx="34" ry="24" />
          <ellipse cx="88" cy="48" rx="44" ry="32" />
          <ellipse cx="132" cy="58" rx="32" ry="24" />
          <ellipse cx="168" cy="53" rx="24" ry="18" />
        </svg>
      </div>
      <div class="absolute top-14 left-1/2 -translate-x-1/2 opacity-70">
        <svg width="180" height="90" viewBox="0 0 180 90" fill="white">
          <ellipse cx="40" cy="50" rx="24" ry="18" />
          <ellipse cx="70" cy="40" rx="34" ry="26" />
          <ellipse cx="105" cy="50" rx="28" ry="22" />
          <ellipse cx="135" cy="46" rx="18" ry="14" />
        </svg>
      </div>
      <div class="absolute bottom-20 left-16 opacity-65">
        <svg width="140" height="80" viewBox="0 0 140 80" fill="white">
          <ellipse cx="34" cy="47" rx="26" ry="20" />
          <ellipse cx="64" cy="40" rx="34" ry="26" />
          <ellipse cx="96" cy="47" rx="26" ry="20" />
          <ellipse cx="120" cy="44" rx="18" ry="14" />
        </svg>
      </div>
      <div class="absolute bottom-12 right-12 opacity-70">
        <svg width="120" height="70" viewBox="0 0 120 70" fill="white">
          <ellipse cx="24" cy="40" rx="18" ry="14" />
          <ellipse cx="44" cy="35" rx="24" ry="18" />
          <ellipse cx="68" cy="45" rx="20" ry="16" />
          <ellipse cx="92" cy="42" rx="14" ry="12" />
        </svg>
      </div>
      <div class="absolute top-10 right-1/2 -translate-x-1/2">
        <div class="h-44 w-44 rounded-full bg-white/20 blur-3xl" />
      </div>
    </div>

    <div class="relative z-10 flex min-h-screen items-center justify-center px-4 py-10">
      <div class="w-full max-w-5xl">
        <div class="grid gap-10 lg:grid-cols-[1.1fr_0.9fr] items-start">
          <!-- Info panel -->
          <section class="space-y-6 text-white">
            <div class="inline-flex rounded-full border border-white/10 bg-white/5 px-4 py-2 text-sm text-sky-200 shadow-lg shadow-sky-500/10 backdrop-blur">
              Beautiful QR code studio
            </div>

            <div class="rounded-[2rem] border border-white/20 bg-white/10 p-10 shadow-2xl shadow-slate-950/30 backdrop-blur-xl ring-1 ring-white/10">
              <div class="space-y-6">
                <div class="space-y-3">
                  <p class="text-sm uppercase tracking-[0.3em] text-sky-300/80">Create, preview, and share</p>
                  <h1 class="text-5xl font-semibold tracking-tight text-white sm:text-6xl">
                    Generate stunning QR codes in seconds
                  </h1>
                  <p class="max-w-xl text-lg leading-8 text-slate-300/90">
                    Type any text or URL, pick a style, and watch your QR update live with a polished preview and gentle glassmorphism textures.
                  </p>
                </div>

                <div class="grid gap-4 sm:grid-cols-2">
                  <div class="rounded-3xl bg-slate-950/90 p-5 border border-white/10 shadow-xl shadow-slate-950/20">
                    <p class="text-sm text-slate-400">Preview</p>
                    <p class="mt-2 text-4xl font-semibold text-white">Live update</p>
                  </div>
                  <div class="rounded-3xl bg-slate-950/90 p-5 border border-white/10 shadow-xl shadow-slate-950/20">
                    <p class="text-sm text-slate-400">Character count</p>
                    <p class="mt-2 text-4xl font-semibold text-white">{{ charCount }}</p>
                  </div>
                </div>
              </div>
            </div>
          </section>

          <!-- QR card -->
          <section class="rounded-[2rem] border border-white/20 bg-white/10 p-8 shadow-2xl shadow-slate-950/35 backdrop-blur-xl ring-1 ring-white/10">
            <div class="space-y-6">
              <div class="space-y-3">
                <p class="text-sm uppercase tracking-[0.32em] text-slate-400">QR code builder</p>
                <h2 class="text-3xl font-semibold text-white">Customize your code</h2>
                <p class="text-slate-400">Switch styles, update text, and copy or scan the latest QR instantly.</p>
              </div>

              <div class="space-y-6">
                <label class="block text-sm font-semibold text-slate-300">Text to encode</label>
                <UInput
                  v-model="text"
                  placeholder="Enter text or URL..."
                  class="w-full rounded-3xl border border-slate-700 bg-slate-950/90 text-white placeholder:text-slate-500"
                  size="lg"
                />

                <div>
                  <label class="block text-sm font-semibold text-slate-300 mb-3">QR style</label>
                  <USelect
                    v-model="variant"
                    :items="variants"
                    placeholder="Select a style..."
                    class="w-full rounded-3xl border border-slate-700 bg-slate-950/90 text-white placeholder:text-slate-500"
                    size="lg"
                  />
                </div>
              </div>

              <div class="rounded-[2rem] border border-white/15 bg-white/10 p-6 shadow-inner shadow-slate-950/15">
                <div class="flex items-center justify-between text-sm text-slate-500 mb-4">
                  <span class="font-medium text-white">QR preview</span>
                  <span class="inline-flex items-center gap-2 rounded-full bg-white/5 px-3 py-1 text-slate-300">
                    <span class="h-2 w-2 rounded-full bg-emerald-400" /> live
                  </span>
                </div>
                <div class="flex justify-center">
                  <div class="rounded-[2rem] bg-white/10 p-6 border border-white/10 shadow-2xl shadow-slate-950/25 transition-transform duration-300 hover:-translate-y-1">
                    <img
                      :src="qr"
                      alt="QR Code"
                      width="300"
                      height="300"
                      class="h-[300px] w-[300px] object-contain"
                    />
                  </div>
                </div>
              </div>

              <div class="grid gap-4 sm:grid-cols-2">
                <div class="rounded-3xl border border-white/10 bg-slate-950/80 p-4 text-slate-300">
                  <p class="text-sm text-slate-500">Current style</p>
                  <p class="mt-2 font-semibold text-white">{{ variant }}</p>
                </div>
                <div class="rounded-3xl border border-white/10 bg-slate-950/80 p-4 text-slate-300">
                  <p class="text-sm text-slate-500">Scannable</p>
                  <p class="mt-2 font-semibold text-white">Yes, right away</p>
                </div>
              </div>
            </div>
          </section>
        </div>

        <footer class="mt-10 text-center text-sm text-slate-500">
          <p>✨ Powered by Nuxt QR Code • Designed for a premium code creation experience</p>
        </footer>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import type { SVGVariant } from 'nuxt-qrcode';

const text = ref('https://nuxt.com');
const variant = ref<SVGVariant>('dots');
const variants = ['default', 'circle', 'pixelated', 'rounded', 'dots'];

const qr = computed(() =>
  useQrcode(text, {
    toBase64: true,
    variant: {
      inner: variant.value,
      marker: 'rounded',
      pixel: variant.value,
    },
    radius: 1,
    blackColor: 'currentColor',
    whiteColor: '#ffffff',
  }).value
);

const charCount = computed(() => text.value.length);
</script>
