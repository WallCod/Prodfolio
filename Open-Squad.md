# 🏢 Open Squad

> **Centro de comando e escritório virtual isométrico em tempo real para orquestração e monitoramento de agentes de IA.**

[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![React](https://img.shields.io/badge/React-18.x-61DAFB?logo=react&logoColor=white)](https://reactjs.org/)
[![Node.js](https://img.shields.io/badge/Node.js-20_LTS-339933?logo=node.js&logoColor=white)](https://nodejs.org/)
[![WebSocket](https://img.shields.io/badge/WebSocket-Live_Sync-blue?logo=socketdotio&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket)
[![Nginx](https://img.shields.io/badge/Nginx-Reverse_Proxy-009639?logo=nginx&logoColor=white)](https://nginx.org/)
[![Status](https://img.shields.io/badge/Status-Em_Produção-brightgreen?style=flat-square)](#)

🌐 **Produção:** [office.alphalabs.fyi](https://office.alphalabs.fyi)

---

## 📖 Sobre o Projeto

O **Open Squad** é a central de observabilidade e visualização em tempo real do ecossistema de inteligência artificial da AlphaLabs. Em vez de telas áridas de log ou listas de processos frios, o Open Squad projeta os agentes de IA autônomos e subagentes (Claude Code, Antigravity, agentes de tarefas) como personagens pixel-art em um **edifício corporativo isométrico contínuo** com total fidelidade visual ao motor do Habblaud.

A plataforma permite acompanhar quem está trabalhando, em qual repositório, quais tarefas estão sendo executadas, histórico de atividades, eventos de Git ao vivo e métricas de desempenho dos modelos de linguagem.

---

## 🧱 Stack Tecnológica

| Camada | Tecnologias |
|---|---|
| **Frontend Web** | React 18, TypeScript, Vite, TailwindCSS, Lucide Icons |
| **Engine Gráfica** | HTML5 Canvas 2D Engine proprietária (renderização isométrica contínua, tilemap de 128 colunas, ordenação de profundidade Y-sort, iluminação e balões de diálogo) |
| **Backend & Servidor** | Node.js, Express, WebSocket (`ws`), TypeScript |
| **Orquestrador de IA** | Runner multi-LLM resiliente com fallback em cascata (Groq `openai/gpt-oss-120b` → DeepSeek → NVIDIA NIM → OpenAI) |
| **Infraestrutura** | VPS Ubuntu 22.04 LTS (DigitalOcean), PM2 (`open-squad`), Nginx com SSL Let's Encrypt |
| **Integração de Eventos** | Hooks de status zero-token/zero-overhead disparados pelas execuções do Claude Code e Antigravity |

---

## 💎 Diferenciais Arquiteturais

### 🏛️ Edifício Corporativo de 8 Colunas e 12 Departamentos
- **Layout Fixo:** Edifício de 128 tiles de largura dividido estruturalmente sem quebras em 12 departamentos funcionais:
  - *Frontend*, *Backend*, *AlphaLabs HQ* (espaço nobre duplo), *Dados*, *DevOps*, *Mobile*, *Segurança*, *Gabinete Executivo* (Founder & Manager), *QA*, *Produto* e *Growth*.
- **Mobiliário Especializado:** Recepção, Copa, Banheiros, Lounge de descanso e mesas operacionais com móveis dinâmicos específicos para cada papel.
- **Rua & Cidade:** Iluminação de postes, carros animados e ambientação na base do edifício.

### 🎭 Renderização Isométrica & Sprites Pixel-Art
- Renderização vetorial e rasterizada sobre Canvas de alta performance com interpolação de movimento suave.
- Sprites de personagens com estados de trabalho: digitando na mesa, andando pelo corredor, balão de fala com status da tarefa atual e comemorações.
- Suporte a geração dinâmica de busto do avatar sob demanda (`avatarCanvas`) para visualização em drawers.

### 📡 Telemetria em Tempo Real via WebSocket & Eventos Git
- Conexão bidirecional mantida via WebSocket seguro (`wss://`).
- **Zero-Token Git Activity:** Detecção automática de comandos git (`push`, `pr`, `merge`, `ci`) executados pelos agentes na máquina local, traduzidos em alertas visuais na sala (chuva de confetes, alarme de deploy).
- Histórico de presenças persistido em `presence-state.json`, garantindo que agentes concluídos permaneçam no histórico da sala de descanso sem sumir após reload.

### 🔍 Inspeção Profunda de Agentes (AgentDrawer & CompanySidebar)
- **Agent Drawer:** Painel lateral direito retrátil com informações detalhadas:
  - Busto pixel-art renderizado em escala 3x.
  - Status em tempo real, papel, sala e tempo de sessão.
  - Botões de câmera cinematográfica: **Centralizar** (move a viewport suavemente) e **Seguir** (câmera acompanha o personagem caminhando pelo edifício).
  - Traços de personalidade, bordão (`catchphrase`), saldo de moedas sociais e vitórias em mini-desafios.
- **Company Sidebar:** Menu à esquerda com busca instantânea de agentes por nome ou departamento, contagem de membros e foco de câmera rápido por sala (`world.focusRoom`).
- **View Insets Compensados:** Ajuste em tempo real do centro visual da câmera para garantir que a abertura de menus laterais nunca cubra o personagem focado.

### 🛡️ Execução Segura & Trust Boundaries
- Separação estrita de privilégios com token dedicado (`OPEN_SQUAD_DISPATCH_TOKEN`).
- Comparação de credenciais em tempo constante (`crypto.timingSafeEqual`) contra ataques de timing.
- Execução de comandos sem invocação de shell (`spawn` direto de argv) com jail de diretório (CWD-jail) e allowlist rigorosa de comandos permitidos.
- Proteção contra SSRF bloqueando faixas privadas (RFC 1918), loopback e endpoints de metadados de nuvem.

### 🧠 Runner Multi-LLM Resiliente
- Suporte a modelos de inferência ultra-rápida (Groq 120B) para processamento de tarefas em ~300ms.
- Fallback automático caso uma API retorne esgotamento de quota ou 429: alterna de forma transparente entre provedores sem interromper tarefas críticas.

---

## 📁 Estrutura do Repositório

```text
open-squad/
├── server/                       # Backend Node.js + WebSocket
│   ├── src/
│   │   ├── index.ts              # Ponto de entrada Express + WS server
│   │   ├── state.ts              # Gerenciador de estado de presenças em memória
│   │   ├── orchestrator/         # Motor de execução segura de tarefas
│   │   │   ├── runner.ts         # Cascata multi-LLM (Groq/DeepSeek/OpenAI)
│   │   │   ├── security.ts       # CWD jail, argv tokenizer & allowlist
│   │   │   └── scheduler.ts      # Agendador seguro opt-in
│   │   └── routes/               # Endpoints REST (/state, /event, /github-event)
│   └── package.json
├── web/                          # Frontend React + Canvas Engine
│   ├── src/
│   │   ├── OfficeCanvas.tsx      # Canvas principal com render loop
│   │   ├── AgentDrawer.tsx       # Gaveta lateral de detalhes e controle de câmera
│   │   ├── CompanySidebar.tsx    # Menu retrátil de departamentos e busca
│   │   ├── officeSnapshot.ts     # Adaptador de estado WS -> Engine Store
│   │   └── world/                # Motor isométrico (layout, render, tiles, city)
│   ├── vite.config.ts
│   └── package.json
└── hooks/                        # Scripts zero-token para Claude Code & Antigravity
    └── report-status.mjs         # Hook de telemetria pré e pós-execução de ferramenta
```

---

## ⚙️ Variáveis de Ambiente (`server/.env`)

```env
PORT=3344
NODE_ENV=production
OPEN_SQUAD_STATUS_TOKEN=sua_chave_secreta_de_telemetria
OPEN_SQUAD_DISPATCH_TOKEN=sua_chave_secreta_de_dispatch
OPEN_SQUAD_ENABLE_SCHEDULER=true

# Provedores de IA para o Orquestrador
GROQ_API_KEY=gsk_...
DEEPSEEK_API_KEY=sk-...
OPENAI_API_KEY=sk-...
```

---

## 🚀 Deploy & Operação na VPS

O serviço roda sob **PM2** atrás do **Nginx** no servidor de produção:

```bash
# Atualização de código e rebuild
cd /home/alpha/apps/open-squad
git pull
cd web && npm install --include=dev && npm run build
cd ../server && npm install --include=dev && npm run build
pm2 restart open-squad
```
