# 🚀 AlphaLabs Audit Pro V3.0

> **Plataforma de auditoria técnica de sites: SEO, segurança e performance com geração de relatórios PDF.**

![Status](https://img.shields.io/badge/Status-Production-green)
![Security](https://img.shields.io/badge/Security-Audit%20Passed-blue)
![Uptime](https://img.shields.io/badge/Uptime-99.9%25-brightgreen)

**[Acessar Plataforma](https://audit.alphalabs.fyi)**

O **AlphaLabs Audit Pro** é uma solução completa para análise de sites, gerando relatórios PDF detalhados com foco em venda de serviços (White-label). A versão V3.0 introduz **segurança de nível bancário**, **monitoramento em tempo real**, **agente de IA no WhatsApp** e **capacidades de auto-cura**.

---

## 🛠️ Stack

- **Frontend:** React 18 + TypeScript + Vite 6 + TailwindCSS + shadcn/ui + Recharts
- **Backend:** Node.js + Express + PostgreSQL
- **Infra:** Docker (node:20-slim + Chromium), Render (frontend + backend), GitHub Actions
- **Agente IA:** LangChain + Groq/OpenAI + MongoDB (RAG) — VPS dedicada

---

## 💎 Diferenciais (V3.0)

### 🔍 Análise de Sites
- Scan de SEO, segurança e performance em tempo real
- Deep Scan via Puppeteer/Chromium: FCP, TTFB, tempo de carregamento, screenshot, erros de console JS
- Métricas de performance proxy com aviso visual quando Puppeteer não executa
- Score geral ponderado (SEO 35% + Segurança 45% + Performance 20%)
- Detecção e listagem de vulnerabilidades críticas

### 📊 Dashboard do Cliente
- Login via chave de licença (sem senha)
- Histórico de auditorias com paginação configurável (10/20/50 por página)
- Gráficos de evolução: AreaChart (score de segurança) + BarChart (distribuição de scores)
- Stats cards: plano, total de scans, score médio, tendência
- Monitoramento contínuo de sites cadastrados
- Página `/config` para alterar nome da conta

### 📄 Relatórios PDF
- Geração client-side (jsPDF + html2canvas), lazy-loaded no clique
- White-label: logo customizado incluído no relatório
- Relatório básico gratuito; relatório técnico completo via pagamento (R$ 29,90)
- Certificado digital incluído nos planos pagos

### 🛡️ Segurança Blindada
- JWT com refresh tokens em HttpOnly cookies
- CSRF protection com Double Submit Cookie (`csrf-csrf`)
- Criptografia AES-256 para dados sensíveis (CPF, Email, Pix)
- Rate limiting por rota (global, deep scan, admin)
- `RESERVED_CREDENTIALS` bloqueia emails de admin no fluxo de cliente
- `ADMIN_PASSWORD` e `JWT_SECRET` obrigatórios via variáveis de ambiente (sem fallback inseguro)

### 💰 Monetização (Built-in)
- Integração Asaas (Pix) com webhook de confirmação automática
- Planos: INDIE (R$ 29,90/mês), AGENCY (R$ 99,90/mês), ENTERPRISE (R$ 299,90/mês)
- Geração automática de licença após pagamento confirmado
- Alerta Telegram/WhatsApp a cada venda

### 🤖 Automação & "Imortalidade"
- **Self-Healing:** Script `auto_update.js` com backup e rollback automático
- **Notificações Telegram:** deploy (início/sucesso/falha), erros 500, login admin, vendas
- **Dependabot inteligente:** auto-merge em patch/minor com CI gate; major sempre manual
- **GitHub Actions:** `deploy-notify.yml` + `deploy-after-dependabot.yml`

### 🧠 Agente de IA no WhatsApp
O Audit Pro é atendido por um agente de IA rodando na VPS, separado do backend do Render. O agente usa **LangChain + Groq/OpenAI** com **RAG em MongoDB** e atende clientes diretamente no WhatsApp via WuzAPI.

> O agente é compartilhado com outras aplicações AlphaLabs mas opera de forma isolada por contexto. Roda com PM2 na porta `3200` na VPS.

Funcionalidades específicas do Audit:

- **🔑 Entrega automática de licença:** após pagamento confirmado, o backend aciona o agente via `POST /internal/deliver-license` — o cliente recebe a chave, o plano e as instruções de acesso no WhatsApp automaticamente, sem intervenção humana
- **💬 Atendimento conversacional:** responde dúvidas sobre a plataforma com base em base de conhecimento (RAG)
- **🖼️ Suporte a imagens:** envia QR codes e capturas de tela como resposta

> O agente é compartilhado com outras aplicações AlphaLabs mas opera de forma isolada por contexto. Roda com PM2 na porta `3200` na VPS.

### 📊 Análise de Concorrência (Novo)
*   **Histórico Completo:** Salva automaticamente todas as comparações realizadas.
*   **Detalhes Profundos:** Modal interativo para visualizar métricas de SEO, Performance e Segurança de ambos os sites lado a lado.
*   **Vencedor Automático:** O sistema declara o vencedor com base no Score Geral.

## 🌐 Deploy (Render)

O projeto usa dois serviços no Render:
- **Backend:** Web Service (Docker), porta 3000
- **Frontend:** Static Site (build Vite)

Push para `main` dispara deploy automático e notificação no Telegram via `deploy-notify.yml`.

---

## 📁 Estrutura do Projeto

```text
AlphaLabs-Auditor-Pro/
├── backend/
│   ├── database/db.js          # PostgreSQL + migrations automáticas
│   ├── routes/                 # auth, payment, analyze, admin, webhook
│   ├── services/               # seo, security, performance, deepScan, analyzeService, notify
│   ├── middleware/             # errorMonitor, auth, CSRF, rate limit
│   ├── utils/                  # scoring, crypto
│   └── Dockerfile
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── dashboard/      # DashboardStats, ScanHistory, MonitoringList
│   │   │   ├── DashboardSection.tsx
│   │   │   ├── MetricCard.tsx
│   │   │   ├── SecurityEvolutionChart.tsx
│   │   │   └── ScoreDistributionChart.tsx
│   │   ├── pages/              # Login, Dashboard, ConfigPage, AdminPanel
│   │   ├── hooks/              # useAuth, useAdmin
│   │   └── utils/              # generatePdf, reportContent
│   └── vite.config.ts
├── .github/
│   ├── dependabot.yml
│   ├── DEPENDABOT_GUIDE.md
│   └── workflows/
│       ├── dependabot-auto-merge.yml
│       ├── deploy-after-dependabot.yml
│       └── deploy-notify.yml
├── docs/
└── .dockerignore               # exclui node_modules do build context (~446MB)
```

---


**Desenvolvido por AlphaLabs Team**
*Versão 3.0 Stable*
