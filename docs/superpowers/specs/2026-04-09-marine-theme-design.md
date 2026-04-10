# Marine Theme — Design Spec

**Date:** 2026-04-09  
**Status:** Approved  

## Context

Onelink currently has one profile template (`Simple.vue`) with a neutral white/slate palette. The goal is to add a second template with a marine Mediterranean aesthetic — turquoise gradients, glassmorphism cards, and clean geometric sans typography — accessible at `/2?data=...`.

The project's architecture explicitly supports this pattern (see CLAUDE.md: *"New templates can be added as new pages (e.g. `pages/2.vue`) using a different template component"*), so `Simple.vue` remains untouched.

---

## Decisions Made

| Topic | Decision |
|-------|----------|
| Aesthetic direction | Mediterranean / Coastal (turquoise, light teal, white) |
| Scope | Profile page only — new template, editor unchanged |
| Typography | Geometric sans (existing system stack: Avenir Next, Roboto, etc.) |
| Tailwind changes | None — existing `teal` and `cyan` palettes are sufficient |

---

## Files to Create

| File | Purpose |
|------|---------|
| `components/Templates/Marine.vue` | New profile template with marine aesthetic |
| `pages/2.vue` | New route that decodes `?data=` and renders `Marine.vue` |

---

## Design Tokens

| Element | Tailwind classes |
|---------|-----------------|
| Page background | `bg-gradient-to-br from-teal-100 to-teal-200` (full height) |
| Name | `text-teal-800 text-xl font-semibold tracking-tight` |
| Description | `text-teal-600 text-sm` |
| Avatar ring | `ring-4 ring-white/70 shadow-lg shadow-cyan-200/50` |
| Social icon wrapper | `bg-white/65 rounded-full shadow-sm shadow-cyan-200/40` |
| Link card | `bg-white/75 border border-white/90 rounded-2xl shadow-sm shadow-teal-300/20` |
| Link icon container | `bg-teal-50 border border-teal-100 rounded-xl` |
| Link label | `text-teal-800 text-sm font-medium` |

---

## Component Structure

### `Marine.vue`

Same props interface as `Simple.vue` — receives `acc` object with identical shape. Renders:

1. **Header**: avatar (with teal ring + glow shadow), name, description
2. **Social icons**: row of circular white-frosted icon buttons (same icons as Simple.vue, tinted teal)
3. **Custom links**: vertical list of glassmorphism cards with icon container + label

### `pages/2.vue`

Mirrors `pages/1.vue` exactly — decodes `route.query.data` via `decodeData` from `utils/transformer.js` and passes result as `acc` prop to `<Templates-Marine />`.

---

## Verification

1. Run `yarn dev`
2. Go to editor at `/`, fill in data and click "Publish"
3. Modify the generated URL: change `/1?data=` to `/2?data=`
4. Confirm the profile renders with the marine theme
5. Verify `pages/1.vue` (Simple template) is unaffected
