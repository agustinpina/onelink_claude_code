# Marine Theme Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a Mediterranean marine profile template accessible at `/2?data=...`, leaving the existing Simple template at `/1` untouched.

**Architecture:** Two new files follow the existing pattern in CLAUDE.md — `components/Templates/Marine.vue` contains the styled template, and `pages/2.vue` decodes the URL data and renders it. No changes to `tailwind.config.js` (existing `teal`/`cyan` palette is sufficient) or any other existing file.

**Tech Stack:** Vue 3, Nuxt 4, Tailwind CSS (teal/cyan palette), Iconify via `nuxt-icon`, `js-base64` (already installed)

---

## File Map

| Action | File | Purpose |
|--------|------|---------|
| Create | `components/Templates/Marine.vue` | Marine profile template (avatar, social icons, link cards) |
| Create | `pages/2.vue` | Route `/2` — decodes `?data=` and renders `<templates-marine>` |

No other files are modified.

---

### Task 1: Create `Marine.vue` template

**Files:**
- Create: `components/Templates/Marine.vue`

- [ ] **Step 1: Create the component**

Create `components/Templates/Marine.vue` with the following content:

```vue
<template>
  <main class="min-h-screen w-full bg-gradient-to-br from-teal-100 to-teal-200 p-4 pt-12">
    <div class="max-w-lg mx-auto space-y-8">

      <div class="text-center">
        <div
          v-if="acc.i"
          class="h-20 w-20 rounded-full overflow-hidden ring-4 ring-white/70 shadow-lg shadow-cyan-200/50 mx-auto"
        >
          <img :src="acc.i" alt="name" class="h-full w-full object-cover" />
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
        <li v-for="(link, id) in acc.ls" :key="id">
          <nuxt-link :to="link.u" target="_blank" v-if="link.l && link.u">
            <div class="flex items-center space-x-3 bg-white/75 border border-white/90 rounded-2xl p-3 shadow-sm shadow-teal-300/20 hover:bg-white/90 transition-colors">
              <div class="flex-shrink-0 flex h-10 w-10 items-center justify-center rounded-xl bg-teal-50 border border-teal-100 text-teal-600">
                <icon v-if="link.i" :name="link.i" class="h-5 w-5" />
                <icon v-else name="ph:link-simple" class="h-5 w-5" />
              </div>
              <p class="font-medium text-sm text-teal-800">{{ link.l }}</p>
            </div>
          </nuxt-link>
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
```

- [ ] **Step 2: Commit**

```bash
git add components/Templates/Marine.vue
git commit -m "feat: add Marine.vue — Mediterranean profile template"
```

---

### Task 2: Create route `pages/2.vue`

**Files:**
- Create: `pages/2.vue`

- [ ] **Step 1: Create the page**

Create `pages/2.vue` — mirrors `pages/1.vue` exactly but renders `<templates-marine>`:

```vue
<template>
  <div>
    <templates-marine v-if="decodedData" :acc="decodedData" />
    <div
      v-else
      class="absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2"
    >
      <base-loading class="h-5 w-5" />
    </div>
  </div>
</template>
<script setup>
import { decodeData } from "../utils/transformer";
const route = useRoute();
const acc = route.query.data;
const decodedData = ref({});
decodedData.value = decodeData(acc);
</script>
<style scoped></style>
```

- [ ] **Step 2: Commit**

```bash
git add pages/2.vue
git commit -m "feat: add /2 route for Marine template"
```

---

### Task 3: Verify manually

**No files modified — verification only.**

- [ ] **Step 1: Start dev server**

```bash
yarn dev
```

Expected: server running at `http://localhost:3000`

- [ ] **Step 2: Generate a test URL**

Go to `http://localhost:3000`, click **Add demo data**, then click **Publish**. A URL like `http://localhost:3000/1?data=<base64>` is copied to clipboard.

- [ ] **Step 3: Test the marine template**

Change `/1?data=` to `/2?data=` in the URL and open it in the browser.

Expected:
- Teal gradient background (`from-teal-100 to-teal-200`)
- Avatar with white ring and cyan shadow
- Social icons as frosted white circles
- Link cards with `rounded-2xl`, white/75 background, teal icon containers

- [ ] **Step 4: Confirm Simple template unaffected**

Open the original `/1?data=<same base64>` URL.

Expected: white background, slate colors — unchanged from before.

---

### Task 4: Deploy

- [ ] **Step 1: Push to main**

```bash
git push origin main
```

- [ ] **Step 2: Verify Vercel deploy**

```bash
vercel ls
```

Expected: newest deployment shows `● Ready`.
