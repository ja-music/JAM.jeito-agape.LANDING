# JA Manager — Landing Page

Página de vendas (estática, single-file) do **JA Manager**, o sistema de gestão do Ministério de Música **Jeito Ágape**. Toda a renda do produto é revertida para o ministério.

> **Stack:** HTML + CSS + JS puro, sem build (single-file, ~92 KB, zero dependências e zero imagens externas — só Google Fonts: *Unbounded* display + *Plus Jakarta Sans* corpo + *Space Mono* dados). Conceito **"NO MESMO TOM"** — a landing *se comporta como o app tocando*. Visual **dark neon vibrante**: preto-violeta `#0A0512` + neon multicolor (violeta/ciano/rosa, lime só no Solo). **Gesto-assinatura:** os 4 públicos (Católico · Evangélico · Banda · Solo) são **presets de EQ** que **recolorem a página inteira** via CSS custom properties (`--accent`/`--glow`) — "mesmo app, afinado pra quem é você". Mockups vivos em CSS/SVG (player Tocando Agora, cifra transpondo em notação BR, telão offline, mixer, escala com "quem já viu", rateio de cachê). **Ecumênico**: estado default neutro; vocabulário de missa só aparece no preset Católico. **Planos em formato de bilheteria** (ingressos), duas trilhas (individual × grupo). Motion tierizado, `prefers-reduced-motion`, contraste AA, mobile 360px sem overflow.

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

## Deploy (Cloudflare Pages — mesmo provedor do app)

Como é estático, o deploy é direto:

```bash
# via Wrangler (Direct Upload)
npx wrangler pages deploy . --project-name=ja-manager-landing

# ou conecte este diretório como um projeto no painel do Cloudflare Pages
# (Build command: vazio | Output dir: / )
```

Sugestão de domínio: `jeitoagape.com.br` (raiz) apontando para a landing, e o app em `app.jeitoagape.com.br` (já existente).

## O que editar com frequência

- **CTAs e links reais**: procure por `TODO: link real` no `index.html` — botões (criar conta / entrar / assinar / convidar / WhatsApp) ainda apontam para âncoras e precisam dos URLs do app/checkout/login.
- **Preços/planos**: seção `#planos` (bilheteria). Todos os valores em R$ são **placeholders marcados `⚠ TODO`** — individual: Cantor grátis + Cantor Pro; grupo: Convidado grátis + Banda + Igreja/Ministério (Recomendado). Toggle Mensal/Anual segue "2 meses grátis" (×10).
- **Contato**: `#contato` (footer) — **WhatsApp do fundador** e **e-mail** são placeholders.
- **Missão**: seção `#missao` (Jeito Ágape).
- **Open Graph**: metas `og:`/`twitter:` prontos, mas falta gerar/hospedar uma imagem `1200×630` e apontar `og:image`.

> Validação visual: dá pra renderizar/checar overflow e console via Chrome headless + CDP (Node 24, sem deps) — útil para garantir mobile 360px sem overflow horizontal e zero erro de console.
