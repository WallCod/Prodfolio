# 🚀 AlphaLabs WhatsApp API

Sistema completo de automação WhatsApp com dashboard web para gerenciamento de instâncias, envio de mensagens, agendamentos, templates, alertas e monitoramento. **Production-ready** com Blue-Green deployment, monitoramento Prometheus e segurança enterprise-grade.

![React](https://img.shields.io/badge/React-18.3-blue)
![TypeScript](https://img.shields.io/badge/TypeScript-5.6-blue)
![Vite](https://img.shields.io/badge/Vite-6.0-646CFF)
![TailwindCSS](https://img.shields.io/badge/TailwindCSS-3.4-38B2AC)
![Node.js](https://img.shields.io/badge/Node.js-20+-green)
![Security](https://img.shields.io/badge/Security-98%2F100-brightgreen)
![Uptime](https://img.shields.io/badge/Uptime-99.9%25-success)
![Endpoints](https://img.shields.io/badge/API%20Endpoints-64+-orange)

**[Acessar Dashboard](https://api.alphalabs.fyi)** | **[API](https://URL_DA_API_AQUI)** | **[Swagger](https://URL_DA_API_AQUI/api-docs)**

---

## ✨ Funcionalidades Completas

### 🔐 Autenticação e Sessões
- Login com cookie httpOnly (sem token no localStorage)
- Refresh token automático (sessão de 24h)
- Proteção CSRF com token rotativo
- Múltiplas sessões simultâneas com revogação
- Persistência de sessão entre reinicializações

### 📲 Gerenciamento de Instâncias WhatsApp
- Multi-instância: crie e gerencie N números WhatsApp
- Conexão via QR Code ou Código de Pareamento (8 dígitos)
- Status em tempo real (conectado/desconectado/autenticado)
- Token único por instância com criptografia AES-256
- Monitoramento de saúde individual por instância

### 💬 Disparador de Mensagens
- Envio individual e em massa
- Validação automática de números no WhatsApp
- Normalização de números brasileiros (+55)
- Anti-ban: limite de 60 msg/hora e 500 msg/dia por instância
- Indicadores visuais de uso com bloqueio automático

### 📝 Templates de Mensagens
- CRUD completo de templates com variáveis dinâmicas (`{{nome}}`, `{{pedido}}`)
- Categorização, busca e filtros avançados
- Duplicação de templates
- Preview com renderização de variáveis
- Estatísticas de uso por template

### 📅 Agendamento de Mensagens
- Agendamento com data/hora específica
- Cancelamento de agendamentos pendentes
- Histórico e filtros por status
- Limpeza automática de agendamentos antigos
- Integração com templates

### 🔗 Webhooks
- Receptor de pedidos e-commerce (`POST /webhook/ecommerce`)
- Receptor de eventos WuzAPI (`POST /webhook/wuzapi`)
- Envio automático de notificações WhatsApp na confirmação de pedidos
- Configuração de webhook URL por instância
- Rate limiting dedicado (10 req/min)

### 🛡️ Sistema de Backups
- Backup automático agendado (via node-cron)
- Backup manual sob demanda
- Retenção configurável (cleanup automático)
- Download de backups
- Estatísticas de armazenamento

### 🔔 Sistema de Alertas
- Alertas automáticos por thresholds configuráveis (CPU, memória, erros)
- Prioridades: Critical, High, Medium, Low
- Acknowledge individual ou em massa
- Configuração de thresholds via API
- Health monitor com verificação forçada

### 📊 Métricas Prometheus
- Integração completa com `prom-client`
- Métricas persistidas em JSON entre reinicializações
- Métricas customizadas: `alphalabs_webhook_*`, `alphalabs_messages_*`
- Counters, Gauges, Histograms e Summaries
- Endpoint `/metrics` compatível com Prometheus/Grafana

### 📈 Analytics
- Visualização de dados por período: 24h / 7 dias / 30 dias
- Gráficos Chart.js: barras, linhas, doughnut
- Métricas: mensagens enviadas, taxa de sucesso, instâncias ativas
- Exportação de dados

### 🏥 Health Checks e Observabilidade
- `/health` - Health check detalhado (memória, uptime, WuzAPI, persistência)
- `/health/ready` - Readiness probe (Kubernetes/Docker)
- `/health/live` - Liveness probe (Kubernetes/Docker)
- `/metrics` - Prometheus scrape endpoint
- `/api-docs` - Swagger UI interativo

### 🚀 Blue-Green Deployment
- Zero downtime com Nginx upstream switching
- Processos PM2: `green` (porta 3100) e `blue` (porta 3101)
- Scripts automáticos: `blue-green-deploy.sh` e `blue-green-switch.sh`
- Health check antes do switch
- Rollback automático em caso de falha

---

## 🎨 Interface — 12 Páginas

| Página | Descrição |
|--------|-----------|
| **Landing** | Apresentação pública com CTAs |
| **Login** | Autenticação segura |
| **Dashboard** | Gerenciamento de instâncias em tempo real |
| **Dispatcher** | Disparador de mensagens individuais/em massa |
| **Templates** | CRUD de templates com variáveis |
| **Scheduler** | Agendamento de mensagens |
| **Webhooks** | Configuração e monitoramento de webhooks |
| **Backups** | Gerenciamento de backups do sistema |
| **Metrics** | Métricas Prometheus em tempo real |
| **Analytics** | Dashboard analítico com gráficos |
| **Alerts** | Central de alertas e configurações |
| **Settings** | Configurações da conta e sistema |

---

## 🛠️ Stack Tecnológica

### Frontend
| Tecnologia | Versão | Uso |
|-----------|--------|-----|
| React | 18.3 | UI Library |
| TypeScript | 5.6 | Type Safety |
| Vite | 6.0 | Build Tool & HMR |
| TailwindCSS | 3.4 | Styling utility-first |
| React Router | 7.13 | SPA routing |
| Chart.js + react-chartjs-2 | 4.5 / 5.3 | Gráficos |
| Lucide React | latest | Ícones |
| React Hot Toast | 2.4 | Notificações |
| Cypress | 15.10 | E2E Testing |

### Backend
| Tecnologia | Versão | Uso |
|-----------|--------|-----|
| Node.js | 20+ | Runtime |
| Express | 4.18 | Framework HTTP |
| prom-client | 15.1 | Prometheus Metrics |
| node-cron | 4.2 | Scheduler |
| Joi | 18.0 | Validação de inputs |
| csurf | 1.11 | CSRF Protection |
| cookie-parser | 1.4 | Cookie httpOnly |
| express-rate-limit | 8.2 | Rate Limiting |
| swagger-jsdoc + swagger-ui | 6.2 / 5.0 | API Docs |
| crypto-js | 4.2 | AES-256 Encryption |
| node-fetch | 2.7 | HTTP cliente (WuzAPI) |
| compression | 1.8 | Gzip response |
| Jest + Supertest | 30.2 | Unit/Integration Testing |

### Infraestrutura
| Componente | Detalhe |
|-----------|---------|
| VPS | DigitalOcean Ubuntu |
| Reverse Proxy | Nginx com SSL/TLS |
| Process Manager | PM2 (green, blue, dashboard, telegram-bot) |
| WhatsApp Engine | WuzAPI (multi-device, porta 8081) |
| Automação | n8n (workflow automation) |
| Deployment | Blue-Green (zero downtime) |

---

## 📡 Endpoints da API — 64+

### Autenticação
```
POST   /admin/login              Login (retorna httpOnly cookie)
POST   /admin/logout             Logout (limpa cookies)
POST   /admin/refresh            Refresh token
GET    /admin/session            Status da sessão atual
GET    /csrf-token               Token CSRF para formulários
```

### Instâncias WhatsApp
```
GET    /admin/users              Listar todas as instâncias
POST   /admin/users              Criar nova instância
DELETE /admin/users/:id          Deletar instância
PUT    /admin/users/:id          Atualizar configurações
```

### WuzAPI Proxy
```
POST   /session/connect          Conectar sessão
GET    /session/status           Status da conexão
GET    /session/qr               QR Code
POST   /session/pairphone        Código de pareamento
POST   /session/disconnect       Desconectar
POST   /user/check               Validar número WhatsApp
POST   /chat/send/text           Enviar mensagem
```

### Estatísticas
```
GET    /admin/stats              Stats de todas as instâncias
GET    /admin/stats/:token       Stats de uma instância
```

### Templates
```
GET    /admin/templates              Listar (com busca/filtro)
POST   /admin/templates              Criar
GET    /admin/templates/:id          Buscar por ID
PUT    /admin/templates/:id          Atualizar
DELETE /admin/templates/:id          Deletar
POST   /admin/templates/:id/duplicate    Duplicar
POST   /admin/templates/:id/render       Renderizar com variáveis
GET    /admin/templates/stats/summary    Estatísticas
```

### Agendamentos
```
GET    /admin/schedules              Listar (com filtros)
POST   /admin/schedules              Criar agendamento
GET    /admin/schedules/:id          Buscar por ID
POST   /admin/schedules/:id/cancel   Cancelar
DELETE /admin/schedules/:id          Deletar
GET    /admin/schedules/stats/summary   Estatísticas
POST   /admin/schedules/cleanup         Limpeza
```

### Backups
```
GET    /admin/backups                    Listar backups
POST   /admin/backups                    Criar backup manual
DELETE /admin/backups/:filename          Deletar backup
GET    /admin/backups/stats              Estatísticas
GET    /admin/backup-scheduler/status    Status do scheduler
POST   /admin/backup-scheduler/backup-now   Backup imediato
POST   /admin/backup-scheduler/cleanup-now  Limpeza imediata
POST   /admin/backup-scheduler/stop         Parar scheduler
POST   /admin/backup-scheduler/start        Iniciar scheduler
```

### Analytics
```
GET    /admin/analytics              Dados analíticos (24h/7d/30d)
```

### Alertas
```
GET    /admin/alerts                          Listar alertas (filtros)
POST   /admin/alerts/:id/acknowledge          Confirmar alerta
POST   /admin/alerts/acknowledge-all          Confirmar todos
GET    /admin/alerts/config                   Config de thresholds
PUT    /admin/alerts/config                   Atualizar thresholds
POST   /admin/health-monitor/check            Forçar health check
```

### Monitoramento
```
GET    /health                   Health check completo
GET    /health/ready             Readiness probe
GET    /health/live              Liveness probe
GET    /metrics                  Prometheus metrics
GET    /prometheus               Alias de /metrics
GET    /admin/metrics            Métricas em JSON
```

### Webhooks
```
POST   /webhook/ecommerce        Receber pedidos e-commerce
POST   /webhook/wuzapi           Receber eventos WuzAPI
```

### Documentação
```
GET    /api-docs                 Swagger UI
GET    /api-docs.json            Swagger JSON spec
```

---

## 🛡️ Segurança (Score: 98/100)

| Camada | Implementação |
|--------|---------------|
| **Autenticação** | httpOnly cookies + refresh token |
| **CSRF** | Token rotativo por requisição |
| **Criptografia** | AES-256 para tokens de instância |
| **Rate Limiting** | 100 req/15min global, 10 req/min webhooks |
| **Validação** | Joi + sanitização de inputs (XSS/injection) |
| **CORS** | Configurado para domínios autorizados |
| **Anti-Ban** | 60 msg/h e 500 msg/d por instância |
| **Headers** | Security headers via Nginx |
| **SSL/TLS** | Certificado Let's Encrypt no Nginx |

---

### Variáveis de Ambiente

```bash
# backend/.env
PORT=3100
WUZAPI_URL=http://localhost:8081
WUZAPI_ADMIN_TOKEN=seu-token-admin-aqui
SESSION_SECRET=string-aleatoria-segura
ENCRYPTION_KEY=chave-aes-256-aqui
NODE_ENV=production
```

Ver `.env.example` no repositório original para todas as variáveis.

---

## 🎯 Scripts

```bash
# Desenvolvimento
npm run start:dev       # Backend + Frontend simultaneamente
npm run backend:dev     # Apenas backend (nodemon)
npm run frontend:dev    # Apenas frontend (Vite HMR)

# Produção
npm run backend:start   # Backend em produção
npm run frontend:build  # Build estático do frontend

# Instalação
npm run install:all     # Instala deps de root + backend + frontend
```

---

## 📁 Estrutura do Projeto

```
Api-AlphaLabs-Zap/
├── backend/
│   ├── middleware/
│   │   ├── auth.js              # Autenticação httpOnly + refresh tokens
│   │   ├── metrics.js           # Prometheus metrics (prom-client)
│   │   └── rateLimiter.js       # Rate limiting por rota
│   ├── utils/
│   │   ├── sanitize.js          # Sanitização XSS/injection
│   │   └── encryption.js        # AES-256 para tokens
│   ├── data/
│   │   ├── instances.json       # Persistência de instâncias
│   │   ├── sessions.json        # Sessões de autenticação
│   │   ├── templates.json       # Templates de mensagens
│   │   ├── schedules.json       # Agendamentos pendentes
│   │   ├── alerts.json          # Estado dos alertas
│   │   └── metrics-persistent.json  # Métricas persistidas
│   ├── backups/                 # Diretório de backups automáticos
│   ├── scripts/
│   │   ├── blue-green-deploy.sh # Deploy zero-downtime
│   │   └── blue-green-switch.sh # Switch de tráfego Nginx
│   ├── webhook-ecommerce.js     # Servidor principal (2130 linhas)
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── LayoutNew.tsx    # Layout responsivo (sidebar + header)
│   │   │   ├── Logo.tsx         # SVG logo
│   │   │   └── ...              # 28 componentes UI
│   │   ├── pages/
│   │   │   ├── Landing.tsx      # Página pública
│   │   │   ├── Login.tsx        # Autenticação
│   │   │   ├── DashboardMain.tsx # Dashboard principal
│   │   │   ├── Dispatcher.tsx   # Disparador de mensagens
│   │   │   ├── Templates.tsx    # Gerenciamento de templates
│   │   │   ├── Scheduler.tsx    # Agendamentos
│   │   │   ├── Webhooks.tsx     # Configuração de webhooks
│   │   │   ├── Backups.tsx      # Sistema de backups
│   │   │   ├── Metrics.tsx      # Métricas Prometheus
│   │   │   ├── Analytics.tsx    # Analytics com gráficos
│   │   │   ├── Alerts.tsx       # Central de alertas
│   │   │   └── Settings.tsx     # Configurações
│   │   ├── services/
│   │   │   └── api.ts           # API client centralizado
│   │   └── App.tsx              # Router e guards de auth
│   ├── cypress/                 # E2E tests
│   └── package.json
├── docs/
│   ├── wiki/                    # Documentação técnica completa
│   ├── deploy/                  # Guias de deploy
│   ├── security/                # Documentação de segurança
│   ├── operations/              # Operações e monitoramento
│   ├── api/                     # Referência da API
│   └── infrastructure/          # Infra: Docker, CDN, WAF
├── scripts/
│   └── deploy/
│       ├── deploy-backend-quick.sh   # Deploy rápido do backend
│       └── deploy-frontend-quick.sh  # Deploy rápido do frontend
├── .github/
│   └── workflows/               # CI/CD GitHub Actions
└── package.json                 # Scripts root
```

---

## 🚀 Deploy — Blue-Green (Zero Downtime)

### Processos PM2 em Produção

| ID | Nome | Porta | Função |
|----|------|-------|--------|
| 1 | telegram-bot | — | Bot Telegram de monitoramento |
| 2 | dashboard | — | VPS Dashboard |
| 12 | green | 3100 | **API ativa** (blue-green) |
| — | blue | 3101 | Standby para deploy |

### Deploy Automático

```bash
# Deploy do backend (atualiza código + reinicia PM2)
bash scripts/deploy/deploy-backend-quick.sh

# Deploy do frontend (build + upload estático)
bash scripts/deploy/deploy-frontend-quick.sh

# Deploy completo zero-downtime na VPS
bash backend/scripts/blue-green-deploy.sh

# Switch manual de tráfego
bash backend/scripts/blue-green-switch.sh [green|blue]
```

### Deploy via GitHub Actions

Configure os secrets no repositório:

- `VPS_HOST` — IP da VPS
- `VPS_USERNAME` — usuário SSH
- `VPS_SSH_KEY` — chave SSH privada

Push para `main` dispara o pipeline automaticamente.

---

## 🏥 Monitoramento

### URLs de Produção

| Recurso | URL |
|---------|-----|
| **API** | `api.alphalabs.fyi` |
| **Dashboard** | `alphalabs.fyi` |
| **Health Check** | `api.alphalabs.fyi/health` |
| **Prometheus** | `api.alphalabs.fyi/metrics` |
| **Swagger** | `api.alphalabs.fyi/api-docs` |

### Health Check Response

```json
{
  "success": true,
  "status": "healthy",
  "uptime": 86400,
  "memory": { "used": "45MB", "limit": "512MB" },
  "wuzapi": "connected",
  "persistence": "ok",
  "version": "2.0.0"
}
```

---

## 📚 Documentação Técnica

| Documento | Descrição |
|-----------|-----------|
| `docs/deploy/BLUE_GREEN_DEPLOYMENT.md` | Deploy zero-downtime |
| `docs/operations/SISTEMA_BACKUP_IMORTAL.md` | Sistema de backups |
| `docs/SISTEMA_ALERTAS.md` | Central de alertas |
| `docs/security/CSRF_PROTECTION.md` | Proteção CSRF |
| `docs/security/ENCRYPTION.md` | Criptografia AES-256 |
| `docs/security/HTTPONLY_COOKIES.md` | Autenticação segura |
| `docs/api/SWAGGER_API.md` | Documentação Swagger |
| `docs/operations/AUTOMACAO_E_MONITORAMENTO.md` | Operações |

---

## 📄 Licença

Este projeto é **privado e proprietário** da **AlphaLabs**.

## 👨‍💻 Autor

**AlphaLabs Development Team**

---

*Desenvolvido com React 18 + TypeScript + Vite + Node.js + Express*
*Versão atual: 2.0.0 — Fevereiro/2026*
