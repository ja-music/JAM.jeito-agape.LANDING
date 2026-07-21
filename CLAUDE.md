# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Sales/landing page for **JA Manager** (`app.jeitoagape.com.br`), a music-repertoire management app (cifras/transposition, setlists, escalas, projeção, ensaios). The page is in **pt-BR**. Tagline/title: **"JA Manager — bota a equipe no mesmo tom"**.

**Positioning (deliberate, keep it):** lead with the *product/features*, not religion. Primary audience is church worship teams, but copy speaks to **ministérios, bandas e grupos** of any kind — evangelical- *and* catholic-friendly, never Catholic-only terms. The app was built inside the **Jeito Ágape** ministry and revenue funds it — kept as ONE compact `#missao` strip, intentionally *not* the dominant theme. (Note: the *product* is a separate brand from the *band* — see `../PTL.jeito-agape.LOPS/docs/MARKETING.md`; product marketing is currently paused.)

## Architecture

One file: [index.html](index.html) (~1270 lines). **No build step, no framework, no dependencies** — HTML + inline `<style>` + inline `<script>`, Google Fonts (**Plus Jakarta Sans** body · **Unbounded** display · **Space Mono** mono).

Current design ("NO MESMO TOM", shipped 2026-07): **dark-neon stage theme** — near-black violet (`--bg-900:#0A0512`, `color-scheme: dark`) with neon accents (`--violet #8B5CF6`, `--cyan #2DE2E6`, `--pink #F0418C`, `--mint`, `--amber`…). All colors/spacing via the `:root` token block — **change tokens, not hardcoded values**.

The signature interaction: **EQ presets** (`#presets`, `data-preset="banda|catolica|evangelica|neutro|solo"`) — clicking a preset **recolors the whole page** and adapts copy, selling "o app se adapta ao seu grupo". There is also a "Now Playing" hero card. Sections in order: `#presets #unifica #cifra #telao #ao-vivo #ensaio #equipe #painel #financeiro #mais #changelog #planos #missao #comecar`.

**Plans (`#planos`)**: trial model is **"1 mês grátis (com cartão)"** (replaced the old free-forever plan — deliberate business decision, 2026-07); prices in the R$ 190–520 range are placeholders until Stripe/billing exists (SaaS backlog phase 3+). CTAs (`criar conta`, `assinar`) still point to `#`/placeholders — the funnel is not wired (see `saas-phase6-gtm.md` in LOPS backlog).

SEO: `robots.txt` + `sitemap.xml` committed; OG image at `https://app.jeitoagape.com.br/assets/og-cover.png`; canonical/JSON-LD in `<head>` (added 2026-07, `feat(seo)`).

## Develop

```bash
python3 -m http.server 4321   # open http://localhost:4321
```
Any static server works. No tests, no lint.

## Deploy — ⚠️ decision pending

This repo's **remote has no deploy workflow**. Locally (untracked!) there are: `.github/workflows/deploy.yml` (GitHub Pages), `CNAME` (`jam.jeitoagape.com.br`), `.nojekyll`, `assets/logo-heart.png` — all from a **discarded local redesign** (backed up in that machine's scratchpad, 2026-07-20). Before committing them, decide: GitHub Pages (these files) vs Cloudflare Pages (`npx wrangler pages deploy .`) — and note `logo-heart.png` is **orphaned** (current design doesn't reference it). Product domain per SEO tags is `app.jeitoagape.com.br`, which conflicts with the old `CNAME` value — reconcile before wiring DNS.

## Editing rules

- All asset paths **relative** (site may be served from a subpath).
- Keep the token-driven theming intact — the EQ presets depend on it.
- Copy changes: keep the inclusive positioning above; product voice is "direto, prático" (not the band's warm-Catholic voice — two brands, two voices).
