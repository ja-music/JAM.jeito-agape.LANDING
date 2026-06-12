# JA Manager — Landing Page

Página de vendas (estática, single-file) do **JA Manager**, o sistema de gestão do Ministério de Música **Jeito Ágape**. Toda a renda do produto é revertida para o ministério.

> Stack: HTML + CSS + JS puro, sem build. Fontes via Google Fonts (*Fraunces* + *Hanken Grotesk*). Tema escuro "litúrgico" (vinho/rosa/dourado) com demo interativo de transposição de cifra no hero.

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

- **Preços/planos**: seção `#planos` no `index.html` (valores `R$ 49` / `R$ 99` são placeholders).
- **Versículo / missão**: seção `#missao`.
- **CTAs**: os botões `href="#"` (criar conta / entrar / assinar) devem apontar para o app ou checkout.
- **Contato/links do footer**.
