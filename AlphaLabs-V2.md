<div align="center">

```
                                ___   __      __           __          __
                               / _ | / /__   / /  ___ _   / /   ___ _ / /  ___
                              / __ |/ / _ \ / _ \/ _  |  / /   / _  // _ \(_-<
                             /_/ |_/_/ .__//_//_/\_,_/  /_/____\__,_//_.__/___/
                                  /_/                  /______/
```

# AlphaLabs V2.0

**Plataforma SaaS Full-Stack para Desenvolvimento de Aplicações Completas**

[![TypeScript](https://img.shields.io/badge/TypeScript-5.8+-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![React](https://img.shields.io/badge/React-18.3-61DAFB?logo=react&logoColor=white)](https://reactjs.org/)
[![Node.js](https://img.shields.io/badge/Node.js-LTS-339933?logo=node.js&logoColor=white)](https://nodejs.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-8.0-47A248?logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![Redis](https://img.shields.io/badge/Redis-Upstash-DC382D?logo=redis&logoColor=white)](https://redis.io/)
[![License](https://img.shields.io/badge/License-ISC-blue.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

[Acessar Plataforma](https://alphalabs.fyi) | [API Docs](https://alphalabs-api.onrender.com/docs) | [Documentação](./docs)

</div>

---

## 📖 Sobre o Projeto

AlphaLabs é uma plataforma **Micro SaaS completa** que permite o desenvolvimento e gerenciamento de aplicações full-stack. Evolução de um sistema focado em automação com IA, agora abrange criação de **frontend, backend, games, apps e soluções de cibersegurança**.

### 🎯 Proposta de Valor

- **Monetização Recorrente**: Sistema de assinaturas integrado com gateway de pagamento Asaas
- **Multi-Tenant**: Suporte para múltiplos clientes com isolamento de dados
- **LGPD Compliant**: 100% em conformidade com a Lei Geral de Proteção de Dados
- **Production-Ready**: Monitoramento completo, backups automáticos e error tracking

---

## ✨ Features Principais

### 🔐 Autenticação & Segurança
- ✅ JWT Authentication com refresh tokens
- ✅ Bcrypt hash (12 rounds) para senhas
- ✅ Rate limiting inteligente (100 req/15min)
- ✅ CSRF Protection
- ✅ Helmet.js para headers de segurança
- ✅ XSS Protection
- ✅ Criptografia AES-256 para dados sensíveis

### 💳 Sistema de Pagamentos
- ✅ Integração completa com Asaas Gateway
- ✅ Assinaturas recorrentes (Mensal/Trimestral/Anual)
- ✅ Webhooks para confirmação de pagamentos
- ✅ Gerenciamento de cobranças e faturas
- ✅ Suporte a PIX, Cartão de Crédito e Boleto

### 👥 Gestão de Clientes
- ✅ Dashboard administrativo completo
- ✅ Perfis de clientes personalizados
- ✅ Sistema de projetos e portfólio
- ✅ Histórico de pagamentos
- ✅ Analytics e métricas em tempo real

### 📊 Monitoramento & Observabilidade
- ✅ Sentry para error tracking e APM
- ✅ Winston logging com rotação diária
- ✅ Health checks automáticos (/api/health)
- ✅ Métricas de sistema, database e negócio
- ✅ Alertas multi-canal (WhatsApp, Telegram, Email)

### 🗄️ Backup & Recuperação
- ✅ Backup automático do MongoDB (diário às 3h)
- ✅ Upload para Google Drive via rclone
- ✅ Retenção de 30 dias para backups diários
- ✅ Backups mensais permanentes
- ✅ Restauração com um comando

### 📱 Notificações
- ✅ Email transacional (Brevo/SendInBlue)
- ✅ WhatsApp API integrada
- ✅ Telegram Bot
- ✅ Alertas críticos com cooldown inteligente

### 🎨 Interface Moderna
- ✅ Design system com shadcn/ui + Radix UI
- ✅ Tema claro/escuro
- ✅ Componentes reutilizáveis
- ✅ Responsivo (mobile-first)
- ✅ Animações com Framer Motion

### 🚀 Performance
- ✅ Redis cache (Upstash) com hit rate tracking
- ✅ Code splitting automático
- ✅ Lazy loading de componentes
- ✅ Otimização de bundle (<1MB gzip)
- ✅ CDN-ready

---

## 🛠️ Tech Stack

### Frontend
```
React 18.3          - UI Library
TypeScript 5.8      - Type Safety
Vite 6.4            - Build Tool & Dev Server
React Router 6.30   - Client-side Routing
Tailwind CSS 3.4    - Utility-first CSS
shadcn/ui           - Component Library
Radix UI            - Unstyled Components
Framer Motion       - Animations
Zustand 4.5         - State Management
React Hook Form     - Form Validation
Zod 3.25            - Schema Validation
TanStack Table      - Data Tables
Recharts 2.15       - Charts & Graphs
Axios 1.13          - HTTP Client
```

### Backend
```
Node.js + Express 5 - Server Framework
TypeScript 5.9      - Type Safety
MongoDB 8.18        - NoSQL Database
Mongoose            - ODM
Redis (Upstash)     - Caching Layer
JWT                 - Authentication
Bcrypt 6.0          - Password Hashing
Helmet 8.1          - Security Headers
CORS                - Cross-Origin Support
Winston 3.19        - Structured Logging
Node-cron 4.2       - Job Scheduling
Nodemailer 7.0      - Email Service
Sentry 10.32        - Error Tracking
```

### DevOps & Infraestrutura
```
Git + GitHub        - Version Control
Render              - Hosting (Backend + Frontend)
MongoDB Atlas       - Database Hosting
Upstash Redis       - Cache Hosting
Cloudinary          - Image Storage
Google Drive        - Backup Storage (rclone)
Sentry.io           - Error Monitoring
```

### Ferramentas de Desenvolvimento
```
ESLint 9.33         - Linting
Prettier 3.6        - Code Formatting
Husky 9.1           - Git Hooks
Lint-staged 16.1    - Pre-commit Linting
Jest 30.2           - Unit Testing
Playwright 1.57     - E2E Testing
Storybook 8.6       - Component Documentation
```

---

## 📁 Estrutura do Projeto

```
AlphaLabs-V.-2.0/
├── backend/                    # Backend Node.js + Express
│   ├── src/
│   │   ├── controllers/        # Business logic
│   │   ├── models/             # Mongoose schemas
│   │   ├── routes/             # API endpoints (23 rotas)
│   │   ├── middleware/         # Auth, validation, rate limiting
│   │   ├── services/           # External services (email, payments)
│   │   ├── jobs/               # Cron jobs (backups, cleanup)
│   │   ├── utils/              # Helpers & utilities
│   │   ├── config/             # Configuration files
│   │   ├── types/              # TypeScript types
│   │   └── app.ts              # Express app setup
│   ├── scripts/                # Automation scripts
│   ├── logs/                   # Winston logs (daily rotation)
│   ├── backups/                # MongoDB backups
│   ├── bin/                    # mongodump & rclone binaries
│   ├── server.ts               # Entry point
│   ├── package.json
│   └── tsconfig.json
│
├── frontend/                   # Frontend React + Vite
│   ├── src/
│   │   ├── components/         # Reusable components
│   │   │   ├── ui/             # shadcn/ui components
│   │   │   ├── common/         # Shared components
│   │   │   ├── payments/       # Payment flows
│   │   │   ├── projects/       # Project management
│   │   │   └── lgpd/           # LGPD compliance
│   │   ├── pages/              # Page components (17 páginas)
│   │   ├── hooks/              # Custom React hooks
│   │   ├── contexts/           # React contexts
│   │   ├── services/           # API clients
│   │   ├── utils/              # Helpers
│   │   ├── types/              # TypeScript types
│   │   ├── layouts/            # Layout components
│   │   ├── styles/             # Global styles
│   │   ├── App.tsx             # Main app component
│   │   └── main.tsx            # Entry point
│   ├── public/                 # Static assets
│   ├── scripts/                # Build & automation scripts
│   ├── package.json
│   ├── vite.config.ts
│   └── tsconfig.json
│
├── shared/                     # Shared types entre frontend/backend
├── docs/                       # Documentação completa
│   ├── BACKUP_SYSTEM.md
│   ├── CHECKLIST_PRODUCAO.md
│   ├── LGPD_COMPLIANCE.md
│   ├── SENTRY_GUIDE.md
│   └── monitoring/
├── .github/                    # GitHub configs
│   └── workflows/              # CI/CD (desabilitado)
├── render.yaml                 # Render deployment config
├── package.json                # Root package (scripts helper)
└── README.md                   # Este arquivo
```

---

## 🔑 Variáveis de Ambiente

### Backend (backend/.env)

| Variável | Descrição | Exemplo | Obrigatório |
|----------|-----------|---------|-------------|
| `NODE_ENV` | Ambiente de execução | `production` / `development` | ✅ |
| `PORT` | Porta do servidor | `5000` | ✅ |
| `MONGO_URI` | Connection string MongoDB | `mongodb+srv://user:pass@cluster...` | ✅ |
| `JWT_SECRET` | Chave secreta JWT | `sua_chave_super_segura_64_chars` | ✅ |
| `JWT_EXPIRES_IN` | Expiração do token | `7d` | ✅ |
| `ENCRYPTION_KEY` | Chave AES-256 (64 hex) | Gerar com `crypto.randomBytes(32).toString('hex')` | ✅ |
| `REDIS_URL` | URL do Redis/Upstash | `redis://user:pass@host:port` | ✅ |
| `FRONTEND_URL` | URL do frontend | `https://seu-app.com` | ✅ |
| `BREVO_API_KEY` | API key Brevo (email) | `xkeysib-...` | ✅ |
| `EMAIL_FROM` | Email remetente | `noreply@alphalabs.fyi` | ✅ |
| `ASAAS_API_KEY` | API key Asaas (min 32 chars) | `sua_api_key_asaas` | ✅ |
| `ASAAS_ENV` | Ambiente Asaas | `sandbox` / `production` | ✅ |
| `SENTRY_DSN` | Sentry error tracking | `https://...@sentry.io/...` | ✅ |
| `CLOUDINARY_CLOUD_NAME` | Cloudinary cloud name | `seu_cloud_name` | ✅ |
| `CLOUDINARY_API_KEY` | Cloudinary API key | `123456789012345` | ✅ |
| `CLOUDINARY_API_SECRET` | Cloudinary API secret | `seu_secret` | ✅ |
| `RCLONE_CONFIG` | Config rclone (Google Drive) | `[gdrive]\ntype = drive\n...` | ⚠️ Opcional |
| `ZAP_API_URL` | WhatsApp API URL | `https://api.alphalabs.fyi` | ⚠️ Opcional |
| `ZAP_TOKEN` | Token WhatsApp API | `seu_token` | ⚠️ Opcional |
| `TELEGRAM_BOT_TOKEN` | Token do bot Telegram | `123456:ABC-DEF...` | ⚠️ Opcional |
| `TELEGRAM_CHAT_ID` | ID do chat Telegram | `123456789` | ⚠️ Opcional |
| `ALERT_WEBHOOK_URL` | Webhook Slack/Discord | `https://hooks.slack.com/...` | ⚠️ Opcional |

### Frontend (frontend/.env)

```bash
VITE_API_URL=http://localhost:5000
VITE_APP_NAME=AlphaLabs
```

**Gerar chaves seguras:**

```bash
# ENCRYPTION_KEY (64 caracteres hex)
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"

# JWT_SECRET (recomendado 64+ caracteres)
node -e "console.log(require('crypto').randomBytes(64).toString('base64'))"
```

---

## 📜 Scripts Disponíveis

### Root (Monorepo)

```bash
npm run start:dev        # Inicia frontend + backend simultaneamente
npm run install:all      # Instala dependências em todos os pacotes
```

### Backend

```bash
npm run dev              # Servidor desenvolvimento (hot reload)
npm start                # Servidor produção
npm run build            # Build TypeScript
npm test                 # Testes unitários + coverage
npm run test:watch       # Testes em modo watch
npm run lint             # ESLint check
npm run lint:fix         # ESLint fix automático
npm run format           # Prettier format
```

### Frontend

```bash
npm run dev              # Servidor desenvolvimento (Vite)
npm run build            # Build produção
npm run preview          # Preview build local
npm test                 # Testes Vitest
npm run test:e2e         # Testes E2E Playwright
npm run lint             # ESLint check
npm run lint:fix         # ESLint fix automático
npm run format           # Prettier format
npm run storybook        # Storybook server
npm run build-storybook  # Build Storybook
```

### Scripts Customizados (Frontend)

```bash
# Generators
npm run create:component # Gerar novo componente
npm run create:page      # Gerar nova página
npm run create:feature   # Gerar nova feature

# Deploy & Health
npm run deploy:smart     # Deploy inteligente
npm run health:custom    # Health check do projeto
npm run health:fix       # Auto-fix de problemas

# Análise
npm run analyze:bundle   # Analisar tamanho do bundle
npm run deps:check       # Checar dependências desatualizadas
npm run security:audit   # Audit de segurança
```

---

## 📡 API Documentation

### Endpoints Principais

#### Autenticação
```
POST   /api/auth/register          - Registrar novo usuário
POST   /api/auth/login             - Login
POST   /api/auth/logout            - Logout
POST   /api/auth/forgot-password   - Recuperar senha
POST   /api/auth/reset-password    - Resetar senha
GET    /api/auth/verify-email      - Verificar email
```

#### Usuários
```
GET    /api/users/profile          - Obter perfil
PUT    /api/users/profile          - Atualizar perfil
DELETE /api/users/account          - Deletar conta (LGPD)
```

#### Projetos
```
GET    /api/projects               - Listar projetos
POST   /api/projects               - Criar projeto
GET    /api/projects/:id           - Detalhes do projeto
PUT    /api/projects/:id           - Atualizar projeto
DELETE /api/projects/:id           - Deletar projeto
```

#### Pagamentos
```
GET    /api/payments               - Histórico de pagamentos
POST   /api/payments/create        - Criar cobrança
GET    /api/payments/:id           - Detalhes de pagamento
POST   /api/webhook/asaas          - Webhook Asaas
```

#### Assinaturas
```
GET    /api/subscriptions          - Listar assinaturas
POST   /api/subscriptions          - Criar assinatura
PUT    /api/subscriptions/:id      - Atualizar assinatura
DELETE /api/subscriptions/:id      - Cancelar assinatura
```

#### Admin
```
GET    /api/admin/users            - Listar todos usuários (admin)
GET    /api/admin/metrics          - Métricas do sistema (admin)
GET    /api/health                 - Health check público
GET    /api/health/detailed        - Health check detalhado (admin)
```

### Autenticação da API

Todas as rotas protegidas requerem JWT no header:

```bash
Authorization: Bearer <seu_token_jwt>
```

Exemplo com curl:

```bash
curl -X GET https://api.alphalabs.fyi/api/users/profile \
  -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
```

---

## 🧪 Testing

### Backend

```bash
cd backend

# Todos os testes
npm test

# Apenas testes unitários
npm run test:unit

# Apenas testes de integração
npm run test:integration

# Watch mode
npm run test:watch

# Coverage
npm run test:coverage
```

### Frontend

```bash
cd frontend

# Testes unitários (Vitest)
npm test

# Testes E2E (Playwright)
npm run test:e2e

# E2E com UI
npm run test:e2e:ui

# E2E debug mode
npm run test:e2e:debug

# Ver relatório E2E
npm run test:e2e:report
```

### Cobertura de Testes

- **Backend:** 85%+ de cobertura
- **Frontend:** 70%+ de cobertura

Veja `docs/COMO_RODAR_TESTES.md` no repositório original para guia completo.

---

## 📄 License

Este projeto está sob a licença **ISC**.

```
ISC License

Copyright (c) 2024-2026 WallCod / AlphaLabs

Permission to use, copy, modify, and/or distribute this software for any
purpose with or without fee is hereby granted, provided that the above
copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
```

---

## 📞 Contato

**Desenvolvedor:** WallCod
**Email:** alphalabsia@gmail.com
**Website:** alphalabs.fyi

---

## 📊 Status do Projeto

| Feature | Status | Observações |
|---------|--------|-------------|
| 🔐 Autenticação | ✅ 100% | JWT + Refresh Tokens |
| 💳 Pagamentos | ✅ 100% | Asaas integrado |
| 📊 Dashboard | ✅ 100% | Analytics completo |
| 🗄️ Backups | ✅ 100% | Diário + Mensal |
| 📱 Notificações | ✅ 100% | Multi-canal |
| 🔒 LGPD | ✅ 100% | Compliance total |
| 🐛 Error Tracking | ✅ 100% | Sentry configurado |
| 📈 Monitoramento | ✅ 100% | Health checks + Métricas |
| 🧪 Testes | 🟡 85% | Meta: 90% |
| 📚 Docs | ✅ 100% | Swagger + Markdown |

---

## 🗺️ Roadmap

### Q1 2026
- [ ] Implementar testes E2E completos (Playwright)
- [ ] Adicionar CI/CD automatizado (GitHub Actions)
- [ ] Migrar para microservices (opcional)
- [ ] Adicionar suporte a múltiplos idiomas (i18n)

### Q2 2026
- [ ] Dashboard analytics avançado (Grafana)
- [ ] Mobile app (React Native)
- [ ] API pública para integrações
- [ ] Marketplace de templates

### Backlog
- [ ] GraphQL API
- [ ] WebSockets para real-time
- [ ] Docker Swarm / Kubernetes
- [ ] Machine Learning para predições

---

<div align="center">

Desenvolvido por WallCod — AlphaLabs

</div>