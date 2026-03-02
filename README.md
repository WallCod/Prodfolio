<div align="center">

# ⚡ Prodfolio

**Documentação técnica das aplicações em produção**

Cada arquivo descreve uma plataforma real, rodando em produção, com stack, arquitetura e funcionalidades detalhadas.

![Status](https://img.shields.io/badge/Status-Em_Produção-brightgreen?style=flat-square)
![Apps](https://img.shields.io/badge/Aplicações-3-blue?style=flat-square)
![Author](https://img.shields.io/badge/Autor-WallCod-black?style=flat-square)

</div>

---

## 📦 Aplicações

### 🏢 [AlphaLabs V2.0](./AlphaLabs-V2.md)

Plataforma Micro SaaS Full-Stack — sistema central do ecossistema AlphaLabs para desenvolvimento e gerenciamento de aplicações. Assinaturas recorrentes, multi-tenant, LGPD compliant e monitoramento completo.

| | |
|---|---|
| 🛠️ **Stack** | React 18.3 · TypeScript · Vite · Node.js · MongoDB · Redis |
| ☁️ **Infra** | Render · MongoDB Atlas · Upstash |
| 🔐 **Auth** | JWT + Refresh Tokens · AES-256 · Rate Limiting |
| 💳 **Pagamentos** | Asaas (Pix · Cartão · Boleto) |

→ [Ver documentação completa](./AlphaLabs-V2.md)

---

### 📲 [AlphaLabs WhatsApp API](./API-AlphaLabs.md)

Sistema de automação WhatsApp com dashboard web completo. Multi-instância, disparador de mensagens, templates com variáveis, agendamentos, webhooks, métricas Prometheus e Blue-Green deployment com zero downtime.

| | |
|---|---|
| 🛠️ **Stack** | React 18.3 · TypeScript · Vite · Node.js · Express |
| ☁️ **Infra** | VPS DigitalOcean · Nginx · PM2 · WuzAPI |
| 📡 **API** | 64+ endpoints · Swagger UI · Prometheus |
| 🚀 **Deploy** | Blue-Green · Zero Downtime · GitHub Actions |

→ [Ver documentação completa](./API-AlphaLabs.md)

---

### 🔍 [AlphaLabs Audit Pro V3.0](./AlphaLabs-Audit-Pro.md)

Plataforma de auditoria SEO, segurança e performance com geração de relatórios PDF white-label. Deep scan com Puppeteer, análise de concorrência, API para CI/CD, self-healing e alertas via Telegram/WhatsApp.

| | |
|---|---|
| 🛠️ **Stack** | TypeScript · React · Node.js · PostgreSQL |
| 🛡️ **Segurança** | AES-256 · CSRF · bcrypt · Score >90 |
| 🤖 **Automação** | Self-Healing · Auto-Deploy · Alertas multi-canal |
| 💰 **Monetização** | Asaas integrado · Webhook de confirmação |

→ [Ver documentação completa](./AlphaLabs-Audit-Pro.md)

---

<div align="center">

Este repositório é um portfólio técnico — sem código-fonte, apenas documentação de arquitetura, stack e decisões técnicas.
Novas aplicações são adicionadas conforme entram em produção.

**[WallCod](https://github.com/WallCod)** · alphalabsia@gmail.com

</div>
