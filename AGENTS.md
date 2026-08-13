# AGENTS.md

## What this is
`mie-jebew-landing.jsx` is a self-contained landing page for "Mie Jebew", a pre-order spicy instant-noodle brand serving the Cimahi/Bandung, Indonesia area. It's a single React component (default-exported `App`) with all CSS injected via `<style>{CSS}</style>` and the hero photo embedded as a base64 JPEG. This folder is now a full Vite + React + Tailwind v4 app that hosts it and is deployed to Vercel.

## Commands
- `npm install` — install dependencies
- `npm run dev` — local dev server
- `npm run build` — production build (Vercel runs this automatically on push)
- `npm run preview` — preview the production build locally
- `npx vercel` / `npx vercel --prod` — deploy preview / production

## Key gotchas
- `Flames` uses `inline-flex gap-1 align-middle` (mie-jebew-landing.jsx:56) — these are Tailwind utility classes; that's why Tailwind v4 is set up via `@tailwindcss/vite` (vite.config.js) with `@import "tailwindcss";` in src/index.css. Everything else is plain custom CSS.
- All styling depends on Google Fonts `@import` (Anton + Plus Jakarta Sans) at the top of the `CSS` string; the host app must allow external font loading.
- Price is hardcoded in two places: `12000 * qty` (line 93) and the "12K ONLY" copy. If the price changes, update both. Business copy (menu, FAQ, price) is Indonesian — keep new copy in Indonesian.
- WhatsApp ordering number is the `WA_LINK` constant (line 19). All order CTAs open WhatsApp with a prefilled message; there is no cart or backend.
- `addOrder` only shows a toast — it does not track orders. Don't assume cart state exists.

## Layout/state
Component state is local and lives in `App` (spice level, quantity, mobile menu, toast). Sections are ordered via scroll anchors: `top`, `menu`, `level`, `tentang`, `faq`. Section order in the file mirrors page order — keep new sections consistent with the `scrollTo` anchors.

## Deploy
Deployed via Vercel (remote: https://github.com/Hem-Portofolio/mie-jebew). Vercel builds from the repo root — keep `index.html`, `vite.config.js`, and `src/` intact. The `.vercel/` and `dist/` folders are git-ignored.
