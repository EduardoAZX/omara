# Dra. Omara — Landing Page

Landing page de captação de leads para a **Dra. Omara**, especialista em **Harmonização Facial e Gerenciamento de Pele**, com foco em rejuvenescimento facial sem aspecto artificial (Zona Sul de São Paulo).

---

## 📁 Estrutura de pastas

```
Omara/
├── index.html            # Estrutura semântica das 6 dobras + modais de Termos/Privacidade
├── style.css              # Design system + componentes + responsividade
├── app.js                  # Reveals, máscara de WhatsApp, validação e submit do form, FAQ, modais
├── README.md                # Este arquivo
├── obrigado.html             # Página de obrigado (redirecionada após o envio do formulário)
├── .htaccess                  # Remoção de .html da URL + headers de segurança
└── assets/
    └── before-after-{1,2,3}-{antes,depois}.webp   # Pares de antes/depois dos 3 procedimentos
```

> Todas as imagens referenciadas em `index.html` apontam para a pasta `assets/`.

---

## 🎨 Design system

| Token              | Valor        | Uso                                          |
|---------------------|--------------|-----------------------------------------------|
| `--c-primary`        | `#B76E79`    | Botões, badges, destaques (dourado-rosé)       |
| `--c-primary-2`      | `#9C5B66`    | Gradientes, itálicos de destaque               |
| `--c-secondary`      | `#F1E9E6`    | Fundos sutis, placeholders                     |
| `--c-accent`         | `#141414`    | CTA escuro                                     |
| `--c-bg`             | `#FAF7F5`    | Fundo padrão (off-white)                       |
| `--c-text`           | `#141414`    | Texto principal (preto)                        |
| `--c-muted`          | `#6B6B6B`    | Texto secundário                               |
| `--c-line`           | `#E6DCDA`    | Bordas e divisores                             |

- **Fontes:** Fraunces (serifada, títulos e itálicos de destaque) + Arimo (sans estilo Helvetica, corpo) — via Google Fonts.
- **Efeitos:** glassmorphism (`backdrop-filter: blur`), sombras suaves em camadas (`--shadow-sm/md/lg/glow`), gradientes dourado-rosé nas seções de Formulário e Rodapé.
- **Favicon:** SVG inline com a inicial **O** sobre o tom primário (dourado-rosé).

---

## 🧩 Seções da LP

### 🟠 Dobra 1 — Hero
- **Imagens:** placeholder (`.hero__photo-fallback`) — inserir foto real da Dra. Omara em consultório.
- CTA único: "Quero minha avaliação personalizada" (`#agendar`).
- Marquee decorativo com os termos dos 3 procedimentos.

### 🟠 Dobra 2 — Transformações Reais
- **Imagens:** `assets/before-after-1..3-antes.webp` / `-depois.webp` — pares reais de antes/depois exibidos lado a lado por card.
- 3 cards: Perda de Sustentação (Recovery Facial), Aparência Cansada (Efeito Descansado), Qualidade da Pele (Gerenciamento de Colágeno).

### 🟠 Dobra 3 — Formulário (captação)
- **Campos:** Nome completo, WhatsApp (máscara `(00) 00000-0000`), E-mail, "Qual sinal mais incomoda você hoje?" (select).
- Validação client-side em `app.js`. Ao validar com sucesso, envia para o webhook do Make e redireciona para `obrigado.html`.
- **Webhook placeholder** — a URL do Make em `MAKE_WEBHOOK_URL` (`app.js`) é herdada do template e precisa ser substituída pela integração real da Dra. Omara.

### 🟠 Dobra 4 — Autoridade (Dra. Omara)
- **Imagens:** placeholder (`.about__photo-fallback`) — inserir foto espontânea/acolhedora da Dra. Omara.
- Copy de autoridade (+20 anos, atendimento individualizado, ANVISA) + CTA escuro.

### 🟠 Dobra 5 — FAQ
- Acordeão com 3 perguntas frequentes (naturalidade, foco do tratamento, discrição).

### 🟠 Dobra 6 — Rodapé
- Localização (Ipiranga — Zona Sul de São Paulo).
- Barra inferior: copyright + links de Termos de Uso / Política de Privacidade (abrem em modal) / Desenvolvido por AZX Performance.

---

## 📜 Termos de Uso & Política de Privacidade

Acessíveis via modal a partir dos links no rodapé (`#openTerms` / `#openPrivacy`). A Política de Privacidade é redigida com base na **LGPD (Lei nº 13.709/2018)**, cobrindo: dados coletados (nome, WhatsApp, e-mail, sinal de interesse), finalidade do tratamento, base legal, compartilhamento, armazenamento/segurança e direitos do titular.

---

## 🔌 Integrações

- **Google Tag Manager:** placeholder `GTM-XXXXXXX` no `<head>` e `<noscript>` de `index.html`/`obrigado.html` — substituir pelo container real antes de publicar. `obrigado.html` já dispara `dataLayer.push({event: 'lead'})` no carregamento, pronto pra virar trigger de conversão no GTM.
- **Webhook (Make/CRM):** placeholder em `app.js` (`MAKE_WEBHOOK_URL`) — substituir antes de publicar.
- **Meta Pixel / CAPI:** não instalado neste projeto.

---

## 📱 Responsividade

| Faixa                | Comportamento                                                   |
|-----------------------|------------------------------------------------------------------|
| **≥ 981px**            | Layouts em 2 colunas (hero, form, about); grid de provas em 2 colunas |
| **820–980px**          | Form e about colapsam para 1 coluna                               |
| **≤ 880px**            | Hero colapsa para 1 coluna, foto centralizada                      |
| **≤ 620px**            | Grid de provas vira 1 coluna                                        |
| **≤ 520px**            | Tipografia e espaçamentos ampliados para leitura mobile; conteúdo centralizado (hero, sobre, formulário, cards, FAQ); inputs a 16px (evita zoom automático do iOS) |
| **≤ 400px**            | Ajustes finos adicionais (stats em 2 colunas)                      |

---

## 🔒 Segurança

- Sem `innerHTML`/`eval`/`document.write` no client-side (sem vetor de XSS via DOM).
- Links externos (`target="_blank"`) sempre com `rel="noopener noreferrer"`.
- Sem conteúdo via `http://` (mixed content).
- `.htaccess` com headers de segurança (X-Frame-Options, CSP, Referrer-Policy, etc.) e remoção de `.html` da URL.
- Validação client-side do formulário em `app.js`; validação server-side deverá ser adicionada junto da integração de envio real.

---

## 🤝 Como contribuir

- **Adicionar uma nova seção:** crie o markup dentro de `index.html` entre duas dobras existentes, atribua um `data-screen-label="NN Nome"` e adicione as classes ao final de `style.css` seguindo o padrão `.nome-secao__elemento`.
- **Mudar a paleta:** edite as custom properties no topo de `style.css` (`:root`).
- **Mudar copy:** todas as strings estão diretamente em `index.html` — sem CMS / template engine.
- **Substituir fotos placeholder:** trocar os blocos `.hero__photo-fallback` e `.about__photo-fallback` por `<img>` reais dentro de `.hero__photo` e `.about__photo-frame`.

---

© 2026 Omara Estética e Saúde — Todos os direitos reservados.
