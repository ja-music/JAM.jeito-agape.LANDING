# JA Manager — Landing Page

Página de vendas (estática, single-file) do **JA Manager**, o sistema de gestão do Ministério de Música **Jeito Ágape**. Toda a renda do produto é revertida para o ministério.

> Stack: HTML + CSS + JS puro, sem build (single-file, ~128 KB, zero dependências e zero imagens externas — só Google Fonts). Fontes: *Bricolage Grotesque* + *Nunito* (alinhadas ao app), com *Fraunces* itálico só no versículo da missão. Visual "dark SaaS litúrgico": slate escuro (`#141416`) + rosa da marca (`#be123c`) + dourado da oferta, com **mockups das telas reais** do app em CSS/SVG (modo projeção no telão, painel com Health Score, mixer multifaixa, cifra com transposição ao vivo, agenda + RSVP por link). Responsivo, acessível e com `prefers-reduced-motion`.

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

- **CTAs e links reais**: procure por `TODO: link real` no `index.html` — os botões (criar conta / entrar / assinar / apoiar) e o contato (`mailto:`/WhatsApp no `#cta-final` e no footer) ainda apontam para âncoras e precisam dos URLs do app/checkout.
- **Preços/planos**: seção `#planos` (valores `R$ 0` / `R$ 49` / `R$ 99` são placeholders, comentados como editáveis).
- **Versículo / missão**: seção `#missao` (Colossenses 3,16).
- **Imagem de compartilhamento (Open Graph)**: os metas `og:`/`twitter:` estão prontos, mas falta gerar/hospedar uma imagem `1200×630` e apontar `og:image` (deixado de fora para manter o single-file 100% portátil).
