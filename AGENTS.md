# AGENTS.md

## What this is
`mie-jebew-landing.jsx` is a self-contained landing page for "Mie Jebew", a pre-order spicy instant-noodle brand serving Cimahi/Bandung, Indonesia. It's a single React component (default-exported `App`) with all CSS injected via `<style>{CSS}</style>` and the hero photo embedded as a base64 JPEG. This repo is a Vite + React + Tailwind v4 app that hosts it and deploys to Vercel. Live: https://jebewin.my.id/

## Entry point / file layout
- `src/main.jsx` — Vite entry; renders `<App />` from the root-level JSX file.
- `mie-jebew-landing.jsx` — the entire app (component + ~220 lines of CSS as a template literal + base64 image). Lives at the repo root, **not** inside `src/`.
- `src/index.css` — only contains `@import "tailwindcss";` (Tailwind v4 setup).
- `public/` — `logo.png` (used as site logo and favicon source), `favicon.png` (copy of logo.png), `robots.txt`, `sitemap.xml`.
- There are **no tests, lint, typecheck, or formatter commands**.

## Commands
Package manager is npm (lockfile present). No monorepo, no workspaces.
- `npm install` — install dependencies
- `npm run dev` — local dev server
- `npm run build` — production build (Vercel runs this on push)
- `npm run preview` — preview the production build locally
- `npx vercel` / `npx vercel --prod` — deploy preview / production

## Key gotchas
- `Flames` uses `inline-flex gap-1 align-middle` (mie-jebew-landing.jsx:56) — Tailwind utility classes. That's why Tailwind v4 is set up via `@tailwindcss/vite` (vite.config.js). Everything else is plain custom CSS.
- All styling lives inside `const CSS = \`...\`` at the bottom of the landing file (line 425+). You're editing a JS template literal — watch for escaped characters and don't break the backtick.
- Fonts load from Google Fonts via `@import` at the top of the CSS string (Anton + Plus Jakarta Sans). The host app must allow external font loading.
- Price is hardcoded in two places: `12000 * qty` (line 93) and the "12K ONLY" copy (line 152). Update both if price changes. Business copy (menu, FAQ, price) is Indonesian — keep new copy in Indonesian.
- WhatsApp number is the `WA_LINK` constant (line 19). All order CTAs open WhatsApp with a prefilled message; there is no cart or backend.
- `addOrder` only shows a toast — it does not track orders. Don't assume cart state exists.

## Layout/state
Component state is local in `App` (spice level, quantity, mobile menu, toast). Sections use scroll anchors: `top`, `menu`, `level`, `tentang`, `faq`. File order mirrors page order — keep new sections consistent with the `scrollTo` anchors.

## Deploy
Vercel (remote: https://github.com/Hem-Portofolio/mie-jebew). Builds from repo root — keep `index.html`, `vite.config.js`, and `src/` intact. `.vercel/` and `dist/` are git-ignored.
