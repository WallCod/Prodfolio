# 🖥️ Dashboard & Observabilidade VPS

> **Central de telemetria em tempo real, gestão de processos e automação self-healing para servidores em nuvem.**

[![Node.js](https://img.shields.io/badge/Node.js-20_LTS-339933?logo=node.js&logoColor=white)](https://nodejs.org/)
[![PM2](https://img.shields.io/badge/PM2-Process_Manager-2B037A?logo=pm2&logoColor=white)](https://pm2.keymetrics.io/)
[![Docker](https://img.shields.io/badge/Docker-Containers-2496ED?logo=docker&logoColor=white)](https://www.docker.com/)
[![Telegram](https://img.shields.io/badge/Telegram_Bot-Alerts_API-26A5E4?logo=telegram&logoColor=white)](https://core.telegram.org/bots)
[![Nginx](https://img.shields.io/badge/Nginx-Reverse_Proxy-009639?logo=nginx&logoColor=white)](https://nginx.org/)
[![Status](https://img.shields.io/badge/Status-Em_Produção-brightgreen?style=flat-square)](#)

🌐 **Produção:** [vps.alphalabs.fyi](https://vps.alphalabs.fyi)

---

## 📖 Sobre o Projeto

O **Dashboard de Monitoramento VPS** é o painel de observabilidade operacional que monitora 24 horas por dia os servidores em produção da AlphaLabs.

Projetado especificamente para ser **ultra-leve e resiliente**, ele elimina a sobrecarga computacional de ferramentas pesadas de monitoramento corporativo (como Grafana/Prometheus/Datadog em instâncias modestas), coletando telemetria diretamente do kernel Linux via chamadas de sistema eficientes e combinando controle de serviços com rotinas automáticas de **auto-recuperação (Self-Healing)**.

---

## 🧱 Stack Tecnológica

| Camada | Tecnologias |
|---|---|
| **Backend & API** | Node.js, Express, JavaScript moderno |
| **Integração de Processos** | PM2 Programmatic API (`pm2 jlist`), Docker Engine CLI, Systemd (`systemctl`) |
| **Telemetria de Sistema** | Sondas nativas de baixo nível via comandos Unix (`top`, `free`, `df`, `uptime`) |
| **Alertas & Notificações** | Bot proprietário no Telegram (`node-telegram-bot-api`), relatórios diários de status |
| **Infra & Rede** | VPS Ubuntu 22.04 LTS (DigitalOcean), Nginx com proxy reverso e SSL Let's Encrypt |

---

## 💎 Diferenciais Arquiteturais

### ⚡ Telemetria Sem Sobrecarga (Zero Heavy TSDB)
- Em vez de manter bancos de séries temporais volumosos ocupando memória RAM e ciclos contínuos de CPU, o backend executa inspeções diretas no subsistema `/proc` e ferramentas nativas.
- Latência de leitura inferior a 50ms para métricas de:
  - Carga de CPU e Load Average (1m, 5m, 15m).
  - Utilização e distribuição de memória RAM (Total, Usada, Livre, Buffer/Cache).
  - Espaço em disco particionado (`df -h`) com gatilho de alerta preventivo aos 85%.

### 🎮 Controle Operacional Seguro de Serviços
- Permite visualizar o status em tempo real, reiniciar, pausar ou recarregar qualquer serviço em execução no servidor.
- **Allowlist Rigorosa (`ALLOWED_ACTIONS`):** Prevenção estrutural de vulnerabilidades de injeção de comandos na API de controle, garantindo que apenas ações homologadas (`restart`, `reload`, `stop`) possam ser executadas nos alvos catalogados.
- **Isolamento de Credenciais:** Bloqueio mandatório de inicialização caso `DASHBOARD_USER` e `DASHBOARD_PASSWORD` não estejam configurados com valores fortes.

### 🤖 Automação Self-Healing & Cães de Guarda (Watchdogs)
A infraestrutura conta com scripts inteligentes de recuperação autônoma:
- **`health-check.sh`:** Avalia a integridade dos endpoints públicos HTTP e reinicia silenciosamente instâncias com resposta 5xx ou timeout.
- **`monitor-alphaclaw.sh`:** Watchdog dedicado que inspeciona o daemon do agente autônomo; em caso de travamento, reinicia o serviço e dispara relatório instantâneo no Telegram alertando se o serviço foi recuperado com sucesso.
- **`pm2-notify.sh`:** Notifica qualquer crash não esperado ou reboots disparados pelo PM2.
- **`weekly-cleanup.sh`:** Manutenção preventiva semanal de rotação e limpeza de logs do PM2 (`pm2 flush`) e Docker prune.

### 📦 Visão Integrada: PM2, Docker e Systemd
Centralização de três paradigmas diferentes de execução sob a mesma interface:
- **Aplicações PM2:** `open-squad`, `agent-alphalabs`, `fiel-doces`, `agent-fiel`, `green`, etc.
- **Containers Docker:** `wuzapi` (WhatsApp Gateway), `n8n` (Workflow automation), `postgres`, `wuzapi-db`.
- **Serviços Nativos Linux:** `alphaclaw` (daemon em Rust rodando sob Systemd).

---

## 📁 Estrutura do Repositório

```text
Dashboard-e-Monitoramento-VPS/
├── server.js                 # Servidor Express com rotas de métricas e controle
├── telegram-bot.js           # Bot interativo do Telegram (/status, /health, /restart)
├── monitoring/
│   ├── health-check.sh       # Watchdog de integridade HTTP dos serviços
│   ├── monitor-alphaclaw.sh  # Script de auto-recuperação do agente autônomo
│   ├── pm2-notify.sh         # Notificador de eventos do PM2
│   └── weekly-cleanup.sh     # Limpeza programada de logs e espaço em disco
└── package.json
```

---

## ⚙️ Variáveis de Ambiente (`.env`)

```env
PORT=7432
DASHBOARD_USER=usuario_administrador
DASHBOARD_PASSWORD=senha_forte_gerada_aleatoria

# Notificações Telegram
TELEGRAM_BOT_TOKEN=...
TELEGRAM_CHAT_ID=...

# URLs Monitoradas para Health Check
API_ALPHALABS_URL=https://api.alphalabs.fyi/health
OFFICE_ALPHALABS_URL=https://office.alphalabs.fyi
FIEL_DOCES_URL=https://fieldocesesalgados.shop
```
