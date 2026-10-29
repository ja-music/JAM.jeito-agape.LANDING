# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Sales/landing page for **JA Manager**, live at **https://jam.jeitoagape.com.br** (the app itself is `app.jeitoagape.com.br`; the band site owns the root `jeitoagape.com.br`), a music-repertoire management app (cifras/transposition, setlists, escalas, projeção, ensaios). The page is in **pt-BR**. Title: **"JA Manager — repertório, escala, ensaio e telão num app só"** (the old tagline "bota a equipe no mesmo tom" survives only as the name of the design concept).

**Copy is checked against the app (2026-10-29 revision).** Every feature claim on the page must be true in the app *today*. Sources of truth, in order: `../JAM.jeito-agape.VUE/src/data/changelog.js` (the user-facing record, 55 releases), `../JAM.jeito-agape.VUE/PRODUCT.md`, `../JAM.jeito-agape.LOPS/CLAUDE.md`. Things the page deliberately does **not** claim because they are not built: "Health Score"/team-health percentages (deleted from the app), live transposition that every device follows (Palco sincronizado, planned), multiple teams/ministries per account (multi-tenant, planned), rehearsal attendance ("quem faltou"), customer counts or testimonials. The `#changelog` feed shows real versions with real dates — refresh it from `changelog.js` when the app ships something sellable. Chords in the mockups use the app's own notation (`C`, `D`, `F#m`, `Gbm`), not "Lá/Ré".

**Positioning (deliberate, keep it):** lead with the *product/features*, not religion. Primary audience is church worship teams, but copy speaks to **ministérios, bandas e grupos** of any kind — evangelical- *and* catholic-friendly, never Catholic-only terms. The app was built inside the **Jeito Ágape** ministry and revenue funds it — kept as ONE compact `#missao` strip, intentionally *not* the dominant theme. (Note: the *product* is a separate brand from the *band* — see `../PTL.jeito-agape.LOPS/docs/MARKETING.md`; product marketing is currently paused.)

## Architecture

One file: [index.html](index.html) (~1030 lines, ~92 KB; all CSS in the single `<style>` in `<head>`, no per-section style blocks). **No build step, no framework, no dependencies** — HTML + inline `<style>` + inline `<script>`, one Google Font: **Montserrat** (variable, `ital,wght@0,400..700;1,400`, `display=swap`, plus a `Montserrat Fallback` `@font-face` over Arial with `size-adjust`/`ascent-override` so the fallback keeps the same metrics). Montserrat is the only family — headings and body share it (`--font-sans`; `--font-display`/`--font-body` are aliases). `--font-mono` is the **system mono stack** (no download) and is used only where the content is data: chords over lyrics in the mockups, the `.mono` inline class, the waveform time. Nothing else may be mono — no uppercase tracked kickers, no mono pills. The old setup (Unbounded + Plus Jakarta Sans + Space Mono) was replaced on 2026-10-29 at the owner's request ("fonte padrão de mercado"): Inter first, then **Montserrat, picked by the owner** from a 9-font comparison the same day. Montserrat is wide, so headings use light negative tracking (`-.02em` h1, `-.015em` h2) and a smaller scale than Inter had (h1 max 3.6rem); the eyebrow labels above headings went in the same pass — the heading carries the section on its own.

Current design ("NO MESMO TOM", shipped 2026-07): **dark-neon stage theme** — near-black violet (`--bg-900:#0A0512`, `color-scheme: dark`) with neon accents (`--violet #8B5CF6`, `--cyan #2DE2E6`, `--pink #F0418C`, `--mint`, `--amber`…). All colors/spacing via the `:root` token block — **change tokens, not hardcoded values**.

The signature interaction: **EQ presets** (`#presets`, `data-preset="banda|catolica|evangelica|neutro|solo"`) — clicking a preset **recolors the whole page** (`--accent`/`--glow`) and swaps copy (the caption under the chips, the telão "momento" and its sentence). Since the 2026-10-29 layout pass the presets are a compact row of chips right under the hero, not a section with four cards. There is also a "Now Playing" hero card.

**Sections in order (v2, 2026-10-29):** hero → `#presets` → `#recursos` (one section, five feature rows with anchors `#cifra #telao #palco #equipe #financeiro`; each row = h3 + one paragraph + four check-bullets + one mockup, sides alternating) → `#mais` (8-cell grid) → `#changelog` (proof) → `#planos` → `#missao` (cream strip, text only) → `#comecar` → footer `#contato`. The v1 sections `#unifica`, `#ao-vivo`, `#ensaio` and `#painel` were cut or merged (`#ao-vivo` + `#ensaio` → `#palco`; `#painel` → `#equipe`) without dropping any claim. **Layout rules:** one background, one surface, 1px borders, neutral shadows (`--shadow-card`); the accent glow is allowed only on the primary CTA, the hero cover, the hero top glow and the recommended plan; one CTA pair in the hero and one in `#comecar`, no per-section CTAs; no glass/backdrop blur outside the sticky nav, no animated background blobs, no grain; the only looping animations are the "tocando agora" dot and the hero chord flip.

**Plans (`#planos`)**: trial model is **"1 mês grátis (com cartão)"** (deliberate business decision, 2026-07). Prices **R$ 19 (Cantor) / 49 (Banda) / 79 (Igreja/Ministério) per month**, annual = 10× (2 months free), were **published by the owner on 2026-10-29**; JSON-LD `offers` match them. **Funnel = waiting list on WhatsApp** (owner's decision, 2026-10-29): there is no signup and no multi-tenancy yet (a new group would see the Jeito Ágape data), so every conversion CTA opens `wa.me/5531991267983` (the band's number, same as the SITE's `_data/contato.yml`) with a pre-filled message naming the plan; "Entrar" and the Convidado ticket go to `app.jeitoagape.com.br/#/login`; the secondary CTA is `mailto:contato@jeitoagape.com.br`. No legal links (the page collects nothing, no analytics). When SaaS phases 2–3 ship, swap the `wa.me` links for signup/checkout (`saas-phase6-gtm.md` in the LOPS backlog).

SEO: canonical, `og:url`, JSON-LD `url`, `robots.txt` and `sitemap.xml` all point at `https://jam.jeitoagape.com.br/`. The share image `assets/og-cover.png` (1200×630) was redrawn on 2026-10-29 in Montserrat with the current headline — it is what WhatsApp shows when the link is shared, so keep it in step with the hero.

## Develop

```bash
python3 -m http.server 4321   # open http://localhost:4321
```
Any static server works. No tests, no lint.

## Deploy — GitHub Pages (live since 2026-10-29)

Every push to `main` runs `.github/workflows/pages.yml`: it copies only what the site serves (`index.html`, `robots.txt`, `sitemap.xml`, `CNAME`, `assets/`) into `_site` and deploys it with `actions/deploy-pages` — same hosting as the band site (`SITE.jeito-agape.JS`). Custom domain `jam.jeitoagape.com.br` (`CNAME` file + the repo's Pages setting). DNS lives in **Cloudflare** (zone `jeitoagape.com.br`): a `CNAME jam → ja-music.github.io` record, **DNS only** (grey cloud) so GitHub can issue the HTTPS certificate. Work straight on `main`; there is no preview environment — check locally first (`python3 -m http.server 4321`).

## Editing rules

- All asset paths **relative** (site may be served from a subpath).
- Keep the token-driven theming intact — the EQ presets depend on it.
- Copy changes: keep the inclusive positioning above; product voice is "direto, prático" (not the band's warm-Catholic voice — two brands, two voices). Conventional SaaS register: headings say plainly what the section is, short sentences, `você`, feature names as the app calls them (Tocadinha, Cronograma, Lâminas, Mural de recados, Caixa), no puns or in-jokes, no competitor names. Before adding a claim, find it in `changelog.js` or `PRODUCT.md`.
- Typography: keep Montserrat as the single family (owner's choice — don't swap it without asking) and the mono stack only for data (see Architecture). Do not reintroduce a display face.
