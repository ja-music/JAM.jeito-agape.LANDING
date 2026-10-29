# JA Manager — Landing Page

Página de vendas (estática, single-file) do **JA Manager**, o sistema de gestão do Ministério de Música **Jeito Ágape**. Toda a renda do produto é revertida para o ministério.

> **Stack:** HTML + CSS + JS puro, sem build (single-file, ~92 KB, zero dependências e zero imagens externas — uma fonte só do Google Fonts: **Montserrat** variável (escolha do dono, 29/10/2026), com fallback métrico em Arial; dados/cifra no mono do sistema, sem download). Conceito **"NO MESMO TOM"** — a landing *se comporta como o app tocando*. Visual **dark neon vibrante**: preto-violeta `#0A0512` + neon multicolor (violeta/ciano/rosa, lime só no Solo). **Gesto-assinatura:** os 4 públicos (Católico · Evangélico · Banda · Solo) são **presets de EQ** que **recolorem a página inteira** via CSS custom properties (`--accent`/`--glow`) — "mesmo app, afinado pra quem é você". Mockups vivos em CSS/SVG (player Tocando Agora, cifra transpondo na notação do app — `C`, `F#m` —, projeção offline, faixas da VS, escala com "quem já viu" e prontidão, rateio de cachê). **Ecumênico**: estado default neutro; vocabulário de missa só aparece no preset Católico. **Planos em formato de bilheteria** (ingressos), duas trilhas (individual × grupo). Motion tierizado, `prefers-reduced-motion`, contraste AA, mobile 360px sem overflow.
>
> **Layout (v2, 2026-10-29):** hero → presets (chips) → `#recursos` com 5 blocos (cifra · projeção · ensaio e palco · escala e página inicial · financeiro; título + parágrafo + 4 marcadores + 1 mockup, lados alternados) → `#mais` (8 itens) → `#changelog` → `#planos` → `#missao` (faixa creme) → `#comecar` → rodapé. Saíram a seção "antes & depois", o painel isolado e os blocos separados de ao-vivo/ensaio (viraram um só, `#palco`); sem CTA por seção, sem vidro/blur, sem blobs animados nem grão; brilho de cor só no CTA principal, na capa do player, no topo do hero e no plano recomendado. Todo o CSS fica num único `<style>` no `<head>`.
>
> **Textos (revisão 2026-10-29):** registro de landing SaaS convencional — o título diz o que o produto é e para quem, cada seção tem um título direto, frases curtas, sem trocadilhos. **Toda funcionalidade citada existe no app hoje**: a fonte é o `changelog.js` do VUE (55 versões) e o `PRODUCT.md`. A seção `#changelog` mostra versões e datas reais — atualize a partir do `changelog.js` quando sair algo vendável. O que **não** está na página porque não existe: "Health Score", transposição que a equipe inteira acompanha (Palco sincronizado, planejado), vários ministérios por conta (multi-tenant, planejado), número de clientes e depoimentos.

## Pré-visualizar localmente

```bash
# qualquer servidor estático serve; ex.:
python3 -m http.server 4321
# abra http://localhost:4321
```

Ou simplesmente abra o `index.html` no navegador.

## Estrutura

```
JAM.jeito-agape.LANDING/
├── index.html   # a página inteira (estilos + scripts inline)
├── assets/      # imagens/ícones futuros
└── README.md
```

## Deploy (GitHub Pages)

No ar em **https://jam.jeitoagape.com.br**. Cada push na `main` publica sozinho (`.github/workflows/pages.yml`, mesmo esquema do site da banda). O DNS fica no Cloudflare: registro `CNAME jam → ja-music.github.io`, só DNS (nuvem cinza).

## O que editar com frequência

- **Lista de espera**: enquanto não existe cadastro, todos os botões de conversão abrem o WhatsApp (31) 99126-7983 com mensagem pronta (`wa.me/5531991267983?text=…`, uma mensagem por plano). "Entrar" e "Já tenho convite" levam ao login do app (`app.jeitoagape.com.br/#/login`).
- **Preços/planos**: seção `#planos` (bilheteria). Valores publicados em 29/10/2026: Cantor R$ 19, Banda R$ 49, Igreja/Ministério R$ 79 por mês; anual = 10× (2 meses grátis). Ao mudar, atualize também o JSON-LD `offers` no `<head>`.
- **Contato**: rodapé (`#contato`) — WhatsApp da banda e `contato@jeitoagape.com.br`.
- **Missão**: seção `#missao` (Jeito Ágape), com link para `jeitoagape.com.br`.
- **Imagem de compartilhamento**: `assets/og-cover.png` (1200×630, Montserrat). É o que aparece no WhatsApp quando o link é enviado — refaça se o título do topo mudar.

> Validação visual: dá pra renderizar/checar overflow e console via Chrome headless + CDP (Node 24, sem deps) — útil para garantir mobile 360px sem overflow horizontal e zero erro de console.
