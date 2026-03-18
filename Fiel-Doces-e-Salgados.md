# 🍬 Fiel Doces & Salgados

E-commerce completo para venda de doces e salgados artesanais.

🌐 **Produção:** [fieldocesesalgados.shop](https://fieldocesesalgados.shop)

---

## 🧱 Stack

**Frontend:** React 19 + TypeScript + Vite + TailwindCSS

**Backend:** Node.js + Express 5 + MongoDB Atlas (Mongoose)

**Deploy:** Render (backend + frontend estático)

**Banco:** MongoDB Atlas — cluster `Cluster0`, banco `fiel`

---

## ✨ Funcionalidades

### 🛒 E-commerce

- Catálogo com imagens via ImageKit
- Carrinho de compras persistente
- Pedidos com mínimo de 20 unidades por produto (Kits Festa: sem mínimo)
- Antecedência mínima de 48h para encomendas
- Entrega ou retirada na loja

### 💳 Pagamentos

- **Mercado Pago:** PIX (5% desconto automático) e Boleto
- **Asaas:** Cartão de crédito (tokenização inline)
- **Pagamento parcial 50/50:** 50% na confirmação, 50% no ato da entrega/retirada

### 🔐 Autenticação

- JWT em cookies httpOnly + refresh tokens
- Confirmação de email (Brevo/Sendinblue via Nodemailer)
- Roles: `user` e `admin`

### 🧑‍💼 Painel Administrativo (`/admin`)

| Rota | Descrição |
| --- | --- |
| `/admin` | Dashboard com métricas |
| `/admin/products` | CRUD de produtos |
| `/admin/orders` | Gestão de pedidos com troca de status |
| `/admin/users` | Gestão de usuários |
| `/admin/sales` | Relatórios de vendas |
| `/admin/reviews` | Moderação de avaliações |
| `/admin/themes` | Personalização visual da loja |
| `/admin/system` | Backups, logs, saúde do sistema |
| `/admin/chatbot` | Base de conhecimento RAG, logs de qualidade, estatísticas |

### 🤖 Chatbot — FielBot (RAG)

- LLM: Groq `llama-3.3-70b-versatile` com fallback automático OpenAI `gpt-4o-mini`
- RAG via MongoDB Atlas Vector Search (embeddings `text-embedding-3-small`, 1536 dims)
- Cardápio injetado dinamicamente a cada conversa — sem reingesta manual
- Contexto do usuário: nome, últimos 10 pedidos, status, valores pagos/pendentes
- Persistência de histórico no Atlas com timestamps (últimas 30 msgs por conversa)
- Memória para anônimos via `sessionId` em cookie httpOnly
- Migração de histórico anônimo → usuário ao fazer login
- TTL automático: histórico some após 90 dias de inatividade
- Logs de qualidade: registra cobertura RAG por mensagem (TTL 60 dias)

### 🔔 Notificações

- Telegram dev: deploy bem-sucedido (boot do servidor) e deploy com falha (polling Render API)
- Email: confirmação de pedido e troca de status (Brevo)
- UptimeRobot: monitoramento de uptime
- Polling Render API a cada 5 min para detectar falha de deploy

### 💾 Sistema de Backups

- Backups diários, semanais e mensais
- Metadados persistidos no MongoDB (sobrevive a redeploys no Render)
- Upload para Google Drive
- Painel admin com status e acionamento manual

---

## ⚙️ Variáveis de Ambiente

### Backend (`backend/.env`)

```env
NODE_ENV=production
PORT=5000
FRONTEND_URL=https://seu-dominio.com

MONGO_URI=mongodb+srv://...

JWT_SECRET=...
JWT_REFRESH_SECRET=...

MERCADO_PAGO_ACCESS_TOKEN=...
ASAAS_API_KEY=...
ASAAS_API_URL=https://www.asaas.com/api/v3  # ou sandbox

EMAIL_USER=...
EMAIL_PASS=...

GROQ_API_KEY=...
OPENAI_API_KEY=...

TELEGRAM_BOT_TOKEN=...
TELEGRAM_CHAT_ID=...

RENDER_API_KEY=...
RENDER_SERVICE_ID=srv-...

API_ALPHA_URL=https://seu-webhook-alphalabs/webhook/ecommerce
```

### Frontend (`.env`)

```env
VITE_BACKEND_URL=https://api.seu-dominio.com
VITE_IMAGEKIT_PUBLIC_KEY=...
VITE_IMAGEKIT_URL_ENDPOINT=...
```

---

## 🛠️ Scripts

### Backend

```bash
cd backend
npm start           # produção
npm run dev         # desenvolvimento (nodemon)
npm run ingest      # popula base de conhecimento RAG no Atlas
```

### Frontend

```bash
npm run dev         # desenvolvimento
npm run build       # build de produção
npm run preview     # preview do build
```

---

## 🧠 Arquitetura do Chatbot RAG

```text
Mensagem do usuário
       │
       ├─► searchKnowledge()  — Atlas Vector Search (top 5 chunks)
       ├─► buildMenuContext() — produtos ativos do banco em tempo real
       ├─► buildUserContext() — pedidos do usuário logado (últimos 10)
       ├─► ChatSession (Atlas) — histórico com timestamps (últimas 30 msgs)
       │
       ▼
   System Prompt montado dinamicamente
       │
       ├─► Groq llama-3.3-70b-versatile  (primário)
       └─► OpenAI gpt-4o-mini            (fallback automático)
```

**Coleções no banco `fiel`:**

- `chatbot_knowledge` — documentos RAG com embeddings (1536 dims, cosine)
- `chatsessions` — histórico por userId ou sessionId, TTL 90 dias
- `chatlogs` — log de qualidade por mensagem, TTL 60 dias

**Search Index no Atlas:**

- Nome: `vector_index`
- Coleção: `chatbot_knowledge`
- Campo: `embedding` (vector, 1536 dims, cosine)

---

## 📡 Rotas da API

### Públicas

| Método | Rota | Descrição |
| --- | --- | --- |
| POST | `/api/auth/login` | Login |
| POST | `/api/auth/register` | Cadastro |
| GET | `/api/products` | Listar produtos |
| POST | `/api/chat` | Chatbot (cookie opcional para contexto) |
| GET | `/api/chat/history` | Histórico do chat |

### Autenticadas

| Método | Rota | Descrição |
| --- | --- | --- |
| POST | `/api/orders` | Criar pedido |
| GET | `/api/orders/my` | Meus pedidos |
| POST | `/api/payments/pix` | Pagamento PIX (MP) |
| POST | `/api/payments/boleto` | Boleto (MP) |
| POST | `/api/asaas/credit-card` | Cartão de crédito (Asaas) |

### Admin (requer role `admin`)

| Método | Rota | Descrição |
| --- | --- | --- |
| GET/POST/PUT/DELETE | `/api/admin/chat/knowledge` | CRUD base RAG |
| GET | `/api/admin/chat/logs` | Logs de qualidade do chatbot |
| GET | `/api/admin/chat/stats` | Estatísticas do chatbot |
| GET | `/api/admin/system/backups` | Listar backups |
| POST | `/api/admin/system/backup` | Acionar backup manual |

---

## 🚀 Deploy

Push para `main` dispara deploy automático no Render.

Ao subir, o servidor notifica o Telegram dev com branch, commit e porta. Se o deploy falhar, o cron de polling da Render API detecta em até 5 minutos e notifica.
