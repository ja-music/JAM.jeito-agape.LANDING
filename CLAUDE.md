# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Sales/landing page for **JA Manager**, live at **https://jam.jeitoagape.com.br** (the app itself is `app.jeitoagape.com.br`; the band site owns the root `jeitoagape.com.br`), a music-repertoire management app (cifras/transposition, setlists, escalas, projeção, ensaios). The page is in **pt-BR**. Title: **"JA Manager — repertório, escala, ensaio e telão num app só"**; hero: **"Seu ministério chega pronto a cada evento."**

**Copy is checked against the app.** Every feature claim on the page must be true in the app *today*. Sources of truth, in order: `../JAM.jeito-agape.VUE/src/data/changelog.js` (the user-facing record), `../JAM.jeito-agape.VUE/PRODUCT.md`, `../JAM.jeito-agape.LOPS/CLAUDE.md`. Things the page deliberately does **not** claim because they are not built: "Health Score"/team-health percentages, live transposition that every device follows (Palco sincronizado, planned), customer counts or testimonials. The proof list ("Feito por quem toca toda semana") shows real versions with real dates — refresh it from `changelog.js` when the app ships something sellable. Chords in the mockups use the app's own notation (`C`, `D`, `F#m`), not "Lá/Ré".

**Positioning (keep it):** lead with the *product/features*, not religion. Primary audience is church worship teams, but copy speaks to **ministérios, bandas e grupos** of any kind — evangelical- *and* catholic-friendly, never Catholic-only terms; the ministry the app was born in is focused on **events** (never "banda para missa"). Since 2026-11 the page has a full section **`#obra` — "Sua assinatura sustenta uma obra."** (owner's request): the app was built inside the **Jeito Ágape** ministry and the subscription funds it.

## Architecture

One file: [index.html](index.html) (~140 KB) — HTML + one `<style>` in `<head>` + one `<script>` at the end. **No build step, no framework, no dependencies.** The 2026-11 version was **generated from the design proposal** (claude.ai design canvas "JAM — nova landing page (funil de vendas)", 2026-11-14…16) and is now the source of truth: edit `index.html` directly. Most styling is **inline** (`style="…"`) as it came out of the canvas; the `<style>` block holds what inline styles cannot do (hover, media queries, the carousel, the FAQ, `.so-largo`/`.so-estreito` breakpoint helpers at 1000 px).

**Look:** graphite ground `#0B0B0D`, surfaces `#141416`/`#17171B`, 1 px borders `#1F1F25`/`#2A2A31`, text `#F4F4F6`/`#B4B4BE`, one accent — the app's **rose `#E11D48`** (text-on-dark tint `#FF637E`) — replacing the old dark-neon violet theme and the EQ presets (both removed). The `#obra` section is the only light surface (`#FBF7F5`).

**Type (pending the team vote, 2026-11-16):** headings **Bricolage Grotesque** (the app's display face) and body **Source Sans 3**, set as CSS variables on the root `div` (`--f-titulo`, `--f-texto`, `--w-titulo`, `--ls-titulo`; `h1,h2,h3,.f-titulo` read them). Changing the pairing = those four variables + the Google Fonts `<link>`. Running text (`p`, `dd`) is **justified with hyphenation** (`hyphens: auto`, `lang="pt-BR"`), owner's request; short card texts stay left-aligned. Mono only for data (chords over lyrics, the import URL).

**Brand mark:** the **same heart as the band site's favicon**, redrawn as a vector and recolored (rose fading to `#6D4458`) — inline SVG in the menu/footer; `assets/favicon.svg` (transparent, lighter gradient under `prefers-color-scheme: dark`), `assets/favicon-32.png`, `assets/apple-touch-icon.png` (on black, iOS needs a background). Never the app's symmetric heart.

**Sections in order:** sticky menu "Setlist" (numbered sections + reading-progress line; hamburger `<details>` on phones) → hero with a **carousel of six real app screens** (`[data-carrossel]`: Home, Palco, Ensaio, Escala, Plano de ensaio, Telão; tabs with a 6 s progress bar, arrows, pause; autoplay off under reduced motion and after any manual navigation; phone screenshots below 1000 px) → trust strip → `#semana` (five aligned cards, one per moment of an event, each with a slice of the app) → `#recursos` with feature rows `#cifra #importar #partitura #escala #ensaio #palco #coordenacao` (sides alternating) → "Também vem junto" → proof (versions) → `#planos` (monthly/annual toggle) → `#obra` → `#perguntas` (9 `<details>`; the JSON-LD `FAQPage` repeats them — change both together) → final CTA → footer.

**Interactive bits** (the script at the end): elements with `data-tpl` carry `data-t-<attr>="… [[key]] …"` templates; `data-acao` buttons flip `estado` (`anual`, `partitura` G/A, `importar` link/nome) and the script re-applies the values (`BASE`/`VARIANTES` tables). Then the menu (current section, progress line, closing the phone menu) and the carousel.

**Screenshots** (`assets/img/telas/*.webp`, computer 2880×1800 and phone 1170×2532) are captures of the **local dev app** with the dev fixtures (`scripts/ui-screenshots` in LOPS, frozen clock) — never production data — with sample texts swapped for the showcase (Missa → casamento, test lyrics → invented lines, role-like names → common names). Re-capture when the app's look changes.

## Plans, trial and funnel

Prices **R$ 19 (Cantor) / 49 (Banda) / 79 (Igreja/Ministério) per month**, annual = 10× (2 months free); JSON-LD `offers` match them. Trial: **7 days free with the credit card registered at sign-up, first charge on day 8** (owner's decision, 2026-11-16; replaced "1 mês grátis"). The self-serve sign-up (Control Tower public route + AbacatePay subscription, lot P5) **does not exist yet**, so every "Testar 7 dias grátis" opens WhatsApp (`wa.me/5531991267983`) with a pre-filled message naming the plan and the origin; the owner releases the ministry from the Control Tower. "Entrar" and the Convidado row go to `app.jeitoagape.com.br/#/login`. When the sign-up ships, swap those links for it (design: the canvas "Começar" board).

**Still placeholders in `[brackets]`** (owner): plan limits (`[2] GB`, `[15]`/`[10] GB`, `[50]`/`[30] GB`, decision D-P1), how the money is used and how the ministry reports it (`#obra`), `[Razão social] · CNPJ` in the footer. Terms and privacy pages do not exist yet (needed before card payments); the page links none.

## Medição, SEO e GEO

- **Analytics is opt-in by constant.** `window.JAM_ANALYTICS = { ga4: '', clarity: '' }` in `<head>`; empty = nothing loads. Fill `ga4` with the **product's own** GA4 measurement ID (never the band's) and `clarity` with the Clarity project id when the owner creates them.
- **Every `wa.me` CTA** carries `data-cta` (`menu | hero | planos | comecar | rodape`), `data-plano` on the plan buttons (`cantor | banda | igreja`) and a pre-filled text that names the plan **and the origin**. The script fires `whatsapp_click` (`cta_location`, `plano`) to `gtag` and `dataLayer`.
- **JSON-LD is one `@graph`** with stable `@id`s: `#organization`, `#website`, `#app` (`SoftwareApplication`, `offers` 19/49/79 as `PreOrder`, `softwareVersion`, `dateModified`, `featureList`) and `#perguntas` (`FAQPage`).
- **Keep in step with releases:** footer "Página atualizada em …" (`<time datetime>`), `softwareVersion`/`dateModified` in the JSON-LD, `lastmod` in `sitemap.xml`, the version line in `llms.txt`, and the proof list.
- `assets/og-cover.png` (1200×630, what WhatsApp shows) repeats the hero headline and the Home screenshot — redo it when either changes.
- **GEO files:** `robots.txt` allows the AI crawlers; `llms.txt` is a hand-written summary copied by the Pages workflow.

## Develop

```bash
python3 -m http.server 4321   # open http://localhost:4321
```
Any static server works. No tests, no lint. Check desktop **and** a 390 px phone (no horizontal scroll), the console, the toggles and the carousel.

## Deploy — GitHub Pages

Every push to `main` runs `.github/workflows/pages.yml`: it copies `index.html`, `robots.txt`, `sitemap.xml`, `llms.txt`, `CNAME` and `assets/` into `_site` and deploys it with `actions/deploy-pages`. Custom domain `jam.jeitoagape.com.br` (`CNAME` + the repo's Pages setting); DNS in **Cloudflare**, `CNAME jam → ja-music.github.io`, **DNS only** (grey cloud) so GitHub issues the HTTPS certificate. *Gotcha:* if the custom domain is saved before the DNS record exists, no certificate is requested — remove the domain and add it back (`echo '{"cname":null}' | gh api -X PUT repos/ja-music/JAM.jeito-agape.LANDING/pages --input -`, then `-f cname=jam.jeitoagape.com.br`). Small fixes go straight to `main`; a redesign goes through a PR (there is no preview environment — check locally first).

## Editing rules

- All asset paths **relative** (site may be served from a subpath).
- Copy: keep the inclusive positioning above; product voice is "direto, prático" (not the band's warm-Catholic voice). Headings say plainly what the section is, short sentences, `você`, feature names as the app calls them (Tocadinha, Cronograma, Lâminas, Mural de recados, Caixa), no puns, no competitor names. Before adding a claim, find it in `changelog.js` or `PRODUCT.md`.
- No eyebrow labels above headings, no glyph icons (inline SVG only), contrast ≥ 4.5:1 for text.
- Images: WebP, with `width`/`height`; only the first carousel slide loads eagerly.
