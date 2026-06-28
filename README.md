# JA Manager — Landing Page

Página de vendas (estática, single-file) do **JA Manager**, o sistema de gestão do Ministério de Música **Jeito Ágape**. Toda a renda do produto é revertida para o ministério.

> **Stack:** HTML + CSS + JS puro, sem build (single-file, ~110 KB, zero dependências e zero imagens externas — só Google Fonts: *Space Grotesk* display + *Inter* corpo + *JetBrains Mono* labels). Visual **dark SaaS ousado**: quase-preto `#0B0A0F`, **um único accent rose** `#F43F6E` (todo CTA) e **âmbar pontual** `#F5B14C` (sagrado/offline/"Recomendado"). Conceito **"PALCO — a interface é a prova"**: cada seção é um mockup vivo das telas reais (telão offline, **cifra transpondo em notação BR**, prova enarmônica lado a lado, mixer/soundcheck, escala + RSVP com "quem já viu", rateio de cachê). **Ecumênico**: fala igual com missa, culto, show e casamento. **Duas trilhas de plano** (individual × grupo). Motion tierizado, `prefers-reduced-motion`, contraste AA e mobile sem overflow horizontal.

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

- **CTAs e links reais**: procure por `TODO: link real` no `index.html` — os botões (criar conta / entrar / assinar / convidar / falar com o fundador) ainda apontam para âncoras e precisam dos URLs do app/checkout/login.
- **Preços/planos**: seção `#planos`. Todos os valores em R$ são **placeholders marcados `⚠ TODO`** (trilha individual: Cantor grátis + Cantor Pro; trilha grupo: Convidado grátis + Banda + Igreja/Ministério). O toggle Mensal/Anual segue a regra de "2 meses grátis" (×10).
- **Contato**: `#contato` (footer) — **WhatsApp do fundador** e **e-mail** são placeholders (`#` / `mailto:` a preencher).
- **Versículo / missão**: seção `#missao` (Colossenses 3,16).
- **Imagem de compartilhamento (Open Graph)**: os metas `og:`/`twitter:` estão prontos, mas falta gerar/hospedar uma imagem `1200×630` e apontar `og:image` (deixado de fora para manter o single-file 100% portátil).

> Validação visual: dá pra renderizar/checar overflow e console via Chrome headless + CDP (Node 24, sem deps) — útil para garantir mobile 360px sem overflow horizontal e zero erro de console.
