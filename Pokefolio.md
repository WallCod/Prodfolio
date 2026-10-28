# 🃏 Pokéfolio

> **Plataforma SaaS para colecionadores de Pokémon TCG com scanner de cartas por Visão Computacional (DINOv2) no navegador, histórico de precificação e gestão de portfólio.**

[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![React](https://img.shields.io/badge/React-18.x-61DAFB?logo=react&logoColor=white)](https://reactjs.org/)
[![ONNX Runtime](https://img.shields.io/badge/ONNX_Runtime_Web-Client_AI-blueviolet?logo=onnx&logoColor=white)](https://onnxruntime.ai/)
[![Node.js](https://img.shields.io/badge/Node.js-20_LTS-339933?logo=node.js&logoColor=white)](https://nodejs.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-47A248?logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![Redis](https://img.shields.io/badge/Redis-Upstash_TLS-DC382D?logo=redis&logoColor=white)](https://upstash.com/)
[![Status](https://img.shields.io/badge/Status-Em_Produção-brightgreen?style=flat-square)](#)

---

## 📖 Sobre o Projeto

O **Pokéfolio** é uma plataforma de inteligência de mercado e gestão de patrimônio voltada a colecionadores e investidores de Pokémon Trading Card Game (TCG).

Diferente de catálogos manuais convencionais, o Pokéfolio incorpora **Visão Computacional diretamente no cliente** para identificação instantânea de cartas através da câmera do celular, além de integrar múltiplos agregadores de preços em tempo real com histórico diário de valorização e métricas patrimoniais.

---

## 🧱 Stack Tecnológica

| Camada | Tecnologias |
|---|---|
| **Frontend Web** | React 18, TypeScript, Vite, Zustand, TailwindCSS, Lucide Icons |
| **Edge AI & Computer Vision** | ONNX Runtime Web, DINOv2 (Meta Vision Transformer) quantizado (~24MB), algoritmo de nitidez por Variância Laplaciana e pHash |
| **Backend API** | Node.js, Express, TypeScript, Mongoose (MongoDB 8) |
| **Cache & Filas** | Upstash Redis (TLS `rediss://`) para rate limit e cache de queries caras |
| **Pagamentos & Monetização** | Gateway Asaas (Cobranças PIX, assinaturas e webhooks com idempotência) |
| **Infra & Observabilidade** | Render, MongoDB Atlas, Sentry APM, Brevo (emails transacionais), Alertas via Zap API (WhatsApp) e Telegram |

---

## 💎 Diferenciais Arquiteturais

### 👁️ Scanner de Cartas por IA no Navegador (Client-Side AI)
- **Zero Latency Server:** O modelo de visão computacional roda diretamente no dispositivo do usuário utilizando WebAssembly/WebGL através do `onnxruntime-web`.
- **Embeddings Pré-computados:** Base de conhecimento vetorial indexada com embeddings DINOv2 de alta dimensionalidade para comparação por similaridade de cosseno em milissegundos.
- **Auto-Capture por Nitidez:** Algoritmo de Variância Laplaciana em tempo real sobre o feed de vídeo da câmera; captura automaticamente o frame apenas quando a carta está nítida, com foco cravado e sem trepidação manual.
- **Tolerância a Ângulos e Variações:** Capaz de diferenciar cartas com mesma arte em versões regulares, *Reverse Holo* e *Secret Rares*.

### 📈 Motor de Inteligência de Preços (10 Cron Jobs)
O backend mantém uma rotina assíncrona de ingestão contínua sem travar as rotas de usuários:
- **Snapshots Diários:** Histórico consolidado de preços mínimos, médios e de mercado por carta.
- **Sincronização Híbrida de Catálogo:** Integração com Pokemontcg.io, Bulbapedia e Serebii para manter conjuntos e dados de coleções atualizados antes dos lançamentos oficiais.
- **Proxy Scraper Resiliente:** Pool de proxies para coleta de cotações em tempo real no mercado nacional (MYP Cards) com chave oficial como fallback.
- **Retenção & Auditoria:** Jobs periódicos de limpeza de cache expirado e reconciliação de integridade do catálogo.

### 💼 Gestão de Patrimônio & Portfólios Múltiplos
- Suporte a múltiplos portfólios por usuário (ex: *Pasta de Trocas*, *Coleção Master Set*, *Cartas Gradadas PSA/BGS*).
- Métricas em tempo real de Lucro/Prejuízo (P&L), Preço Médio Pago e Valor Total de Mercado.
- Painel analítico com gráficos de pizza por raridade/coleção e curvas de valorização temporal.

### 🛡️ Segurança & Blindagem de Produção
- **Criptografia AES-256-GCM:** Chave `ENCRYPTION_KEY` obrigatória no boot para criptografar documentos fiscais (CPF) e dados sensíveis dos colecionadores.
- **devGuard:** Middleware de guarda que inspeciona o connection string do MongoDB no startup e aborta instantaneamente qualquer script de seed ou deleção em massa se o banco for de produção.
- **Backups Automatizados:** Rotina diária via GitHub Actions gerando dumps do MongoDB para armazenamento redundante em nuvem.

---

## 📁 Estrutura do Repositório

```text
poke-folio/
├── backend/
│   ├── src/
│   │   ├── jobs/               # 10 agendadores (price snapshots, sync, audit)
│   │   ├── lib/                # Cache Redis, crypto GCM, MYP scraper, notifications
│   │   ├── models/             # Mongoose schemas (Card, Portfolio, Payment, User)
│   │   ├── routes/             # Endpoints REST da API
│   │   ├── services/           # Regras de negócio (asaas, email, tcg)
│   │   └── server.ts           # Boot do Express com guardas de segurança
│   ├── data/
│   │   └── embeddings.bin      # Embeddings DINOv2 pré-computados das cartas
│   └── scripts_py/             # Pipeline Python para geração e quantização de pesos
└── frontend/
    ├── src/
    │   ├── pages/              # Dashboard, Catalog, Collection, Scanner, Prices
    │   ├── store/              # Zustand (useCollection, usePortfolios, useAchievements)
    │   ├── lib/                # ONNX runtime wrapper, Laplacian variance, pHash
    │   └── admin/              # Sub-aplicação administrativa completa
    └── vite.config.ts
```

---

## ⚙️ Variáveis de Ambiente (`backend/.env`)

```env
PORT=5000
NODE_ENV=production
MONGODB_URI=mongodb+srv://.../pokefolio_prod
REDIS_URL=rediss://default:...@upstash.io:6379
JWT_SECRET=super_secret_jwt_key
ENCRYPTION_KEY=64_character_hex_aes_256_gcm_key

# Provedores de Dados TCG
POKEMONTCG_API_KEY=...
MYP_PROXY_HOST=...
MYP_PROXY_USER=...
MYP_PROXY_PASS=...

# Pagamentos & Notificações
ASAAS_API_KEY=$aact_...
ASAAS_WEBHOOK_TOKEN=...
BREVO_API_KEY=xkeysib-...
TELEGRAM_BOT_TOKEN=...
TELEGRAM_CHAT_ID=...
```
