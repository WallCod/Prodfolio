<div align="center">

# ⚡ Prodfolio

**Documentação técnica das aplicações e plataformas em produção**

Cada arquivo descreve uma plataforma real, rodando em produção, com stack detalhada, arquitetura, segurança e decisões de engenharia.

![Status](https://img.shields.io/badge/Status-Em_Produção-brightgreen?style=flat-square)
![Apps](https://img.shields.io/badge/Aplicações-10-blue?style=flat-square)
![Author](https://img.shields.io/badge/Autor-WallCod-black?style=flat-square)

</div>

---

## 🧭 Índice de Categorias

- [🏢 SaaS & Plataformas Centrais](#-saas--plataformas-centrais)
- [🤖 Agentes Autônomos, IA & Observabilidade](#-agentes-autônomos-ia--observabilidade)
- [🃏 Plataformas de TCG, Visão Computacional & Torneios](#-plataformas-de-tcg-visão-computacional--torneios)
- [🛍️ E-commerce & Atendimento Inteligente](#️-e-commerce--atendimento-inteligente)

---

## 🏢 SaaS & Plataformas Centrais

### 🏢 [AlphaLabs V2.0](./AlphaLabs-V2.md)

Plataforma Micro SaaS Full-Stack — sistema central do ecossistema AlphaLabs para desenvolvimento e gerenciamento de aplicações. Assinaturas recorrentes, multi-tenant, LGPD compliant e monitoramento completo.

| | |
|---|---|
| 🛠️ **Stack** | React 18.3 · TypeScript · Vite · Node.js · Express 5 · MongoDB · Redis |
| ☁️ **Infra** | Render · MongoDB Atlas · Upstash Redis · Cloudflare |
| 🔐 **Auth** | JWT + Refresh Tokens · AES-256 · Rate Limiting · Sentry |
| 💳 **Pagamentos** | Asaas (Pix · Cartão · Boleto) |

→ [Ver documentação completa](./AlphaLabs-V2.md)

---

### 📲 [AlphaLabs WhatsApp API](./API-AlphaLabs.md)

Sistema de automação WhatsApp com dashboard web completo. Multi-instância, disparador em massa, templates com variáveis, agendamentos, webhooks, métricas Prometheus e Blue-Green deployment com zero downtime.

| | |
|---|---|
| 🛠️ **Stack** | React 18.3 · TypeScript · Vite · Node.js · Express · WuzAPI |
| ☁️ **Infra** | VPS DigitalOcean (Ubuntu) · Nginx · PM2 · Docker |
| 📡 **API** | 64+ endpoints · Swagger UI · Prometheus Metrics |
| 🚀 **Deploy** | Blue-Green · Zero Downtime · GitHub Actions |

→ [Ver documentação completa](./API-AlphaLabs.md)

---

### 🔍 [AlphaLabs Audit Pro V3.0](./AlphaLabs-Audit-Pro.md)

Plataforma de auditoria SEO, segurança e performance com geração de relatórios PDF white-label. Deep scan via Puppeteer/Chromium, análise de concorrência lado a lado, self-healing e entrega automatizada de licenças via IA no WhatsApp.

| | |
|---|---|
| 🛠️ **Stack** | React 18 · TypeScript · Vite · Node.js · PostgreSQL (Neon) |
| 🛡️ **Segurança** | AES-256-GCM · CSRF Double Submit · bcrypt · Rate Limiting |
| 🤖 **Automação** | Self-Healing · Agente WhatsApp RAG · Alertas multi-canal |
| 💰 **Monetização** | Asaas integrado · Webhooks automáticos |

→ [Ver documentação completa](./AlphaLabs-Audit-Pro.md)

---

## 🤖 Agentes Autônomos, IA & Observabilidade

### 🏛️ [Open Squad](./Open-Squad.md)

Centro de comando e escritório virtual isométrico em tempo real com paridade visual Habblaud. Renderiza a presença e atividade de agentes de IA em um edifício corporativo de 12 departamentos, com telemetria WebSocket ao vivo, detecção de eventos Git e orquestrador multi-LLM resiliente.

| | |
|---|---|
| 🛠️ **Stack** | React 18 · TypeScript · HTML5 Canvas 2D Engine · Node.js · WebSocket |
| 🧠 **IA Engine** | Cascata multi-LLM (Groq 120B `gpt-oss-120b` · DeepSeek · NIM · OpenAI) |
| 📡 **Telemetria** | WebSocket seguro · Eventos Git zero-token · Histórico persistido |
| 🛡️ **Segurança** | CWD-jail · Spawn sem shell · Timing-safe token auth · SSRF guard |

→ [Ver documentação completa](./Open-Squad.md)

---

### 🦀 [AlphaClaw & Ecossistema de Voz Neural](./AlphaClaw.md)

Agente autônomo multicanal de alta performance compilado em Rust com loop ReAct e segurança fail-closed, integrado a um pipeline de síntese neural de voz 24/7 que envia áudio gravado nativo (PTT) para o WhatsApp e Alexa Voice Skills.

| | |
|---|---|
| 🛠️ **Stack** | Rust (Edição 2021) · Tokio Async · Systemd Daemon · Edge Neural TTS |
| 🔌 **Canais** | WhatsApp (WuzAPI PTT) · Telegram · Alexa Custom Skill (AWS Lambda) |
| 🛡️ **Segurança** | Fail-Closed PolicyLevel · Workspaces isolados por usuário |
| 🎙️ **Áudio** | Síntese de fala neural humanizada · Higienização fonética em runtime |

→ [Ver documentação completa](./AlphaClaw.md)

---

### 🖥️ [Dashboard & Observabilidade VPS](./Dashboard-VPS.md)

Central de telemetria em tempo real, gestão de processos e automação self-healing para os servidores em nuvem da AlphaLabs. Monitora hardware, daemons PM2, containers Docker e serviços Systemd com zero sobrecarga de bancos temporais pesados.

| | |
|---|---|
| 🛠️ **Stack** | Node.js · Express · PM2 API · Docker Engine · Systemd · Bash |
| ⚡ **Métricas** | CPU, RAM, Disk (`df -h`), Load Average direto do kernel Linux (<50ms) |
| 🤖 **Self-Healing** | Watchdogs automáticos (`health-check.sh`, `monitor-alphaclaw.sh`) |
| 🚨 **Alertas** | Bot interativo dedicado no Telegram com comandos remotos seguros |

→ [Ver documentação completa](./Dashboard-VPS.md)

---

## 🃏 Plataformas de TCG, Visão Computacional & Torneios

### 🃏 [Pokéfolio](./Pokefolio.md)

Plataforma SaaS para colecionadores de Pokémon TCG com scanner de cartas por Visão Computacional (DINOv2) diretamente no navegador, histórico diário de precificação de mercado e gestão patrimonial de coleções.

| | |
|---|---|
| 🛠️ **Stack** | React 18 · TypeScript · Zustand · Node.js · MongoDB Atlas · Redis Upstash |
| 👁️ **Client AI** | ONNX Runtime Web · DINOv2 quantizado · Auto-capture por Variância Laplaciana |
| 📈 **Jobs** | 10 cron jobs em background (Snapshots de preços · Sync Bulbapedia/MYP) |
| 🔐 **Segurança** | AES-256-GCM para documentos · Proteção `devGuard` contra wipe |

→ [Ver documentação completa](./Pokefolio.md)

---

### 🏆 [Liga Itabuna TCG](./Liga-Itabuna-TCG.md)

Plataforma comunitária completa para gestão de torneios oficiais de Pokémon TCG, rankings competitivos da temporada, leilões em tempo real com anti-sniping e chaveamento automático via Sistema Suíço.

| | |
|---|---|
| 🛠️ **Stack** | React 18 · TanStack Router & Query · Node.js · Express · MongoDB |
| ⚔️ **Torneios** | Algoritmos proprietários: Sistema Suíço (Buchholz/Sonneborn-Berger) & Grupos |
| 💰 **Pagamento** | Gerador algorítmico local de PIX (taxa zero para a comunidade) |
| 🔄 **Automação** | 5 schedulers in-process para encerramento de leilões e rankings |

→ [Ver documentação completa](./Liga-Itabuna-TCG.md)

---

### 🏪 [Itacaré TCG](./Itacare-TCG.md)

Marketplace multi-vendedor especializado em cartas colecionáveis e produtos de Pokémon TCG com checkout Mercado Pago, portal administrativo de lojistas e rastreamento de entregas.

| | |
|---|---|
| 🛠️ **Stack** | React 18 · React Router · Context API · Node.js · Express · MongoDB |
| 💳 **Checkout** | Mercado Pago Checkout Pro (PIX · Cartão · Boleto) + Webhooks |
| 🏬 **Vendedores** | Portal dedicado para lojistas, controle de estoque e fotos via Cloudinary |
| 🛡️ **Validação** | Validação fiscal de CPF/CNPJ e degradação graciosa de serviços |

→ [Ver documentação completa](./Itacare-TCG.md)

---

## 🛍️ E-commerce & Atendimento Inteligente

### 🍬 [Fiel Doces & Salgados](./Fiel-Doces-e-Salgados.md)

E-commerce completo para venda de doces e salgados artesanais. Catálogo com ImageKit, carrinho persistente, pagamentos divididos 50/50, backups para Google Drive e chatbot conversacional RAG com Groq e OpenAI.

| | |
|---|---|
| 🛠️ **Stack** | React 19 · TypeScript · Vite · Node.js · Express 5 · MongoDB Atlas |
| 🤖 **Chatbot** | FielBot RAG · Groq `llama-3.3-70b` · Fallback OpenAI · Atlas Vector Search |
| 💳 **Pagamentos** | Mercado Pago (Pix com 5% desc) · Asaas (Cartão) · Sinal 50/50 |
| ☁️ **Infra** | Render · MongoDB Atlas · Cloudflare Edge Proxy & SSL |

→ [Ver documentação completa](./Fiel-Doces-e-Salgados.md)

---

<div align="center">

Este repositório é um portfólio técnico — sem código-fonte proprietário, apenas documentação de arquitetura, stack e decisões de engenharia.
Novas aplicações são adicionadas e atualizadas conforme entram em produção.

**[WallCod](https://github.com/WallCod)** · alphalabsia@gmail.com

</div>
