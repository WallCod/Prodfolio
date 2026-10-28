# 🏆 Liga Itabuna TCG

> **Plataforma comunitária completa para gestão de torneios oficiais de Pokémon TCG, rankings competitivos, leilões em tempo real e pareamento automático (Sistema Suíço).**

[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![React](https://img.shields.io/badge/React-18.x-61DAFB?logo=react&logoColor=white)](https://reactjs.org/)
[![TanStack Router](https://img.shields.io/badge/TanStack_Router-File_Based-FF4154?logo=react&logoColor=white)](https://tanstack.com/router)
[![TanStack Query](https://img.shields.io/badge/TanStack_Query-Async_State-FF4154?logo=reactquery&logoColor=white)](https://tanstack.com/query)
[![Node.js](https://img.shields.io/badge/Node.js-20_LTS-339933?logo=node.js&logoColor=white)](https://nodejs.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-47A248?logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![Status](https://img.shields.io/badge/Status-Em_Produção-brightgreen?style=flat-square)](#)

---

## 📖 Sobre o Projeto

A **Liga Itabuna TCG** é a plataforma oficial de gestão competitiva da comunidade de Pokémon TCG no sul da Bahia.

Criada para substituir planilhas manuais e softwares legados de chaveamento, o sistema cobre todo o ciclo de vida de uma liga: desde inscrições automatizadas com pagamentos PIX instantâneos locais, passando pelo **gerenciamento de rodadas com emparceiramento suíço em tempo real**, até leilões de cartas raras, rankings históricos da temporada e mural de conquistas da comunidade.

---

## 🧱 Stack Tecnológica

| Camada | Tecnologias |
|---|---|
| **Frontend Web** | React 18, TypeScript, Vite, TanStack Router (rotas tipadas baseadas em arquivos), TanStack Query, TailwindCSS |
| **Backend API** | Node.js, Express, TypeScript, Mongoose (MongoDB 8) |
| **Motor de Torneios** | Algoritmos proprietários em TypeScript puro para pareamento Suíço (*Swiss System*) e Fase de Grupos |
| **Pagamentos Comunitários** | Motor local de geração de payload EMV e QR Code PIX (taxa zero, sem intermediário) |
| **Agendadores In-Process** | 5 cron jobs internos (`setInterval`/scheduler) para regras de negócio autônomas |
| **Mídia & Notificações** | Cloudinary (CDN de imagens de torneios), Brevo (Email), WhatsApp (Zap API) e Telegram |

---

## 💎 Diferenciais Arquiteturais

### ⚔️ Motor Proprietário de Torneios (Swiss System & Group Stage)
Diferente de sistemas que dependem de APIs externas engessadas, o pareamento foi codificado de raiz com regras oficiais do circuito competitivo:
- **Swiss System (`swiss.ts`):** Emparceiramento dinâmico rodada a rodada agrupando jogadores por pontuação de vitórias/empates/derrotas.
- **Prevenção de Rematch:** Algoritmo que garante que dois competidores nunca se enfrentem duas vezes na mesma fase suíça.
- **Critérios de Desempate Oficiais:** Cálculo automático de pontuação por resistência Buchholz e Sonneborn-Berger.
- **Controle de Mesas e Bye:** Atribuição automática de mesas físicas na sala e gestão inteligente de *Bye* (vitória automática para o jogador sem par em rodadas ímpares).

### 🏷️ Leilões em Tempo Real & Mecanismo Anti-Sniping
- Sistema de leilão de cartas com lances mínimos incrementais e timer regressivo.
- **Anti-Sniping:** Se um lance for feito no último minuto do leilão, o cronômetro é estendido automaticamente por mais 2 minutos, evitando bots e garantindo disputas limpas.
- Fechamento autônomo do leilão gerenciado por agendador de segundo plano, atribuindo o vencedor e disparando notificação direta para o comprador.

### 💰 Pagamento Local PIX com Custo Zero
- A plataforma não depende de taxas percentuais de gateways de pagamento para repasse comunitário.
- Gerador algorítmico do padrão Banco Central EMVCo (`lib/pix.ts`): monta a string "Copia e Cola" e renderiza o QR Code SVG diretamente no cliente, permitindo confirmação rápida e conferência simplificada pelo organizador.

### 🔄 5 Schedulers In-Process em Background
Sem a complexidade ou custo de filas pesadas como Celery ou BullMQ, o Express mantém rotinas leves em background:
1. **Auction Close:** Varredura periódica para encerrar leilões que atingiram o deadline.
2. **Weekly League Report:** Consolidação semanal de pontos e envio de resumo para a comunidade.
3. **Ranking Sync:** Recálculo e ordenação de pontuações elo da temporada.
4. **Mural Reminder:** Atualização e rotação de destaques e avisos da semana.
5. **Event Status Transition:** Transição automática de status de torneio (Inscrições Abertas → Em Andamento → Concluído).

### 🛡️ Proteção de Integridade & devGuard
- **devGuard:** Trava de segurança no boot que intercepta comandos destrutivos (como remoção de registros de torneios passados ou seeds acidentais) e bloqueia a execução caso detecte a URL do cluster de produção.
- **Histórico & Hall da Fama:** Preservação imutável de campeões e registros de torneios passados.

---

## 📁 Estrutura do Repositório

```text
liga-itabuna-TCG/
├── backend/
│   ├── src/
│   │   ├── controllers/        # Controladores por domínio (auction, tournament, ranking, user)
│   │   ├── lib/
│   │   │   ├── swiss.ts        # Motor de pareamento Sistema Suíço
│   │   │   ├── groupStage.ts   # Algoritmo de fase de grupos
│   │   │   ├── pix.ts          # Gerador de payload Pix EMV
│   │   │   └── devGuard.ts     # Proteção do banco de produção
│   │   ├── models/             # 19 Mongoose Schemas (Auction, Tournament, Round, Bracket, User)
│   │   ├── routes/             # Rotas da API REST
│   │   └── server.ts           # Inicialização e disparo dos 5 schedulers
├── frontend/
│   ├── src/
│   │   ├── routes/             # Rotas baseadas em arquivos via TanStack Router
│   │   ├── components/
│   │   │   ├── admin/          # Painéis administrativos por módulo
│   │   │   ├── tournament/     # Chaveamentos visuais, emparceiramento e mesas
│   │   │   └── auction/        # Cards de leilão com timer ao vivo
│   │   └── lib/
│   │       ├── pix-qr.tsx      # Renderizador do QR Code Pix
│   │       └── api.ts          # Cliente HTTP integrado com TanStack Query
│   └── vite.config.ts
```

---

## ⚙️ Variáveis de Ambiente (`backend/.env`)

```env
PORT=5000
NODE_ENV=production
MONGODB_URI=mongodb+srv://.../liga_itabuna_prod
JWT_SECRET=sua_chave_jwt_secreta
JWT_REFRESH_SECRET=sua_chave_refresh

# Integrações de Mídia & Alertas
CLOUDINARY_CLOUD_NAME=...
CLOUDINARY_API_KEY=...
CLOUDINARY_API_SECRET=...
BREVO_API_KEY=xkeysib-...

# Notificações
ZAP_API_URL=https://api.alphalabs.fyi
ZAP_API_TOKEN=...
TELEGRAM_BOT_TOKEN=...
TELEGRAM_CHAT_ID=...
```
