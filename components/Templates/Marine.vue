<template>
  <main class="min-h-screen w-full bg-gradient-to-br from-teal-100 to-teal-200 p-4 pt-12">
    <div class="max-w-lg mx-auto space-y-8">

      <div class="text-center">
        <div
          v-if="acc.i"
          class="h-20 w-20 rounded-full overflow-hidden ring-4 ring-white/70 shadow-lg shadow-cyan-200/50 mx-auto"
        >
          <img :src="acc.i" :alt="acc.n" class="h-full w-full object-cover" />
        </div>
        <h1 v-if="acc.n" class="text-xl font-semibold tracking-tight mt-4 text-teal-800">
          {{ acc.n }}
        </h1>
        <p v-if="acc.d" class="text-sm mt-2 text-teal-600">
          {{ acc.d }}
        </p>
      </div>

      <div
        v-if="!allSocialLinksAreEmpty"
        class="flex items-center justify-center flex-wrap gap-2"
      >
        <a v-if="acc.f" :href="acc.f" target="_blank" rel="noopener noreferrer"
           class="flex h-9 w-9 items-center justify-center rounded-full bg-white/65 shadow-sm shadow-cyan-200/40 text-teal-600 hover:bg-white/90 transition-colors">
          <icon name="ph:facebook-logo-duotone" class="h-5 w-5" />
        </a>
        <a v-if="acc.t" :href="acc.t" target="_blank" rel="noopener noreferrer"
           class="flex h-9 w-9 items-center justify-center rounded-full bg-white/65 shadow-sm shadow-cyan-200/40 text-teal-600 hover:bg-white/90 transition-colors">
          <icon name="ph:twitter-logo-duotone" class="h-5 w-5" />
        </a>
        <a v-if="acc.ig" :href="acc.ig" target="_blank" rel="noopener noreferrer"
           class="flex h-9 w-9 items-center justify-center rounded-full bg-white/65 shadow-sm shadow-cyan-200/40 text-teal-600 hover:bg-white/90 transition-colors">
          <icon name="ph:instagram-logo-duotone" class="h-5 w-5" />
        </a>
        <a v-if="acc.tg" :href="acc.tg" target="_blank" rel="noopener noreferrer"
           class="flex h-9 w-9 items-center justify-center rounded-full bg-white/65 shadow-sm shadow-cyan-200/40 text-teal-600 hover:bg-white/90 transition-colors">
          <icon name="ph:telegram-logo-duotone" class="h-5 w-5" />
        </a>
        <a v-if="acc.w" :href="`https://wa.me/${acc.w}`" target="_blank" rel="noopener noreferrer"
           class="flex h-9 w-9 items-center justify-center rounded-full bg-white/65 shadow-sm shadow-cyan-200/40 text-teal-600 hover:bg-white/90 transition-colors">
          <icon name="ph:whatsapp-logo-duotone" class="h-5 w-5" />
        </a>
        <a v-if="acc.y" :href="acc.y" target="_blank" rel="noopener noreferrer"
           class="flex h-9 w-9 items-center justify-center rounded-full bg-white/65 shadow-sm shadow-cyan-200/40 text-teal-600 hover:bg-white/90 transition-colors">
          <icon name="ph:youtube-logo-duotone" class="h-5 w-5" />
        </a>
        <a v-if="acc.e" :href="`mailto:${acc.e}`" target="_blank" rel="noopener noreferrer"
           class="flex h-9 w-9 items-center justify-center rounded-full bg-white/65 shadow-sm shadow-cyan-200/40 text-teal-600 hover:bg-white/90 transition-colors">
          <icon name="ph:envelope-duotone" class="h-5 w-5" />
        </a>
        <a v-if="acc.gh" :href="acc.gh" target="_blank" rel="noopener noreferrer"
           class="flex h-9 w-9 items-center justify-center rounded-full bg-white/65 shadow-sm shadow-cyan-200/40 text-teal-600 hover:bg-white/90 transition-colors">
          <icon name="ph:github-logo-duotone" class="h-5 w-5" />
        </a>
        <a v-if="acc.l" :href="acc.l" target="_blank" rel="noopener noreferrer"
           class="flex h-9 w-9 items-center justify-center rounded-full bg-white/65 shadow-sm shadow-cyan-200/40 text-teal-600 hover:bg-white/90 transition-colors">
          <icon name="ph:linkedin-logo-duotone" class="h-5 w-5" />
        </a>
      </div>

      <ul class="space-y-3">
        <li v-for="(link, id) in acc.ls" :key="id" v-if="link.l && link.u">
          <a :href="link.u" target="_blank" rel="noopener noreferrer">
            <div class="flex items-center space-x-3 bg-white/75 border border-white/90 rounded-2xl p-3 shadow-sm shadow-teal-300/20 hover:bg-white/90 transition-colors">
              <div class="flex-shrink-0 flex h-10 w-10 items-center justify-center rounded-xl bg-teal-50 border border-teal-100 text-teal-600">
                <icon v-if="link.i" :name="link.i" class="h-5 w-5" />
                <icon v-else name="ph:link-simple" class="h-5 w-5" />
              </div>
              <p class="font-medium text-sm text-teal-800">{{ link.l }}</p>
            </div>
          </a>
        </li>
      </ul>

    </div>
  </main>
</template>

<script setup>
const props = defineProps({
  acc: {
    type: Object,
    required: true,
  },
});

const allSocialLinksAreEmpty = computed(() => {
  return (
    !props.acc.f &&
    !props.acc.t &&
    !props.acc.ig &&
    !props.acc.tg &&
    !props.acc.w &&
    !props.acc.y &&
    !props.acc.e &&
    !props.acc.gh &&
    !props.acc.l
  );
});
</script>

<style scoped></style>
