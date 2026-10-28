# 🦀 AlphaClaw & Ecossistema de Voz Neural

> **Agente autônomo multicanal de alta performance compilado em Rust com loop ReAct, segurança fail-closed e pipeline de síntese neural de voz 24/7.**

[![Rust](https://img.shields.io/badge/Rust-2021_Edition-DEA584?logo=rust&logoColor=white)](https://www.rust-lang.org/)
[![Tokio](https://img.shields.io/badge/Tokio-Async_Runtime-black?logo=rust&logoColor=white)](https://tokio.rs/)
[![Systemd](https://img.shields.io/badge/Systemd-Production_Daemon-CC2200?logo=linux&logoColor=white)](https://systemd.io/)
[![Edge TTS](https://img.shields.io/badge/Edge_Neural_TTS-Zero_Cost_Voice-0078D7?logo=microsoft&logoColor=white)](https://azure.microsoft.com/services/cognitive-services/text-to-speech/)
[![WhatsApp](https://img.shields.io/badge/WhatsApp-WuzAPI_PTT-25D366?logo=whatsapp&logoColor=white)](https://github.com/asternic/wuzapi)
[![Status](https://img.shields.io/badge/Status-Em_Produção-brightgreen?style=flat-square)](#)

---

## 📖 Sobre o Projeto

O **AlphaClaw** é o agente autônomo inteligente central do ecossistema AlphaLabs. Desenvolvido em **Rust**, foi projetado como um binário nativo estático de altíssima eficiência e baixo consumo de memória, capaz de operar ininterruptamente como daemon do sistema Linux (`systemd`).

O projeto integra inteligência artificial conversacional a um **pipeline neural de áudio e voz em tempo real**, permitindo que o agente interaja de forma fluida via WhatsApp (enviando mensagens de voz nativas gravadas no microfone), Telegram e comandos de voz com Alexa.

---

## 🧱 Stack Tecnológica

| Camada | Tecnologias |
|---|---|
| **Núcleo do Agente** | Rust (Edição 2021), Tokio Async Runtime, Reqwest, Serde, Async-Trait |
| **Pipeline de Voz & Áudio** | Edge Neural TTS (vozes neurais naturais em português), conversão de áudio OGG/Opus PTT, WuzAPI Gateway |
| **Arquitetura Cognitiva** | Loop ReAct assíncrono com chamada e validação de ferramentas (*Tool-calling*) |
| **Busca & Memória** | Mecanismo de busca híbrida (BM25 lexical + embeddings vetoriais) com workspaces por usuário |
| **Modelos de Linguagem** | Roteamento dinâmico: Ollama local + fallback em cascata para Anthropic, Groq, OpenAI e DeepSeek |
| **Infraestrutura** | VPS Ubuntu (DigitalOcean), gerenciado via **Systemd Daemon** com watchdog de auto-cura |

---

## 💎 Diferenciais Arquiteturais

### 🔌 Arquitetura Multicanal Desacoplada (`Gateway/Channel Trait`)
O núcleo do agente não possui acoplamento rígido com nenhuma rede social ou protocolo de chat. Ele implementa uma abstração assíncrona limpa:
- **Trait Unificada:** Todo canal de comunicação implementa 4 métodos básicos assíncronos (`name`, `start`, `send`, `health_check`).
- **Chave de Sessão Canônica:** As conversas são indexadas no formato universal `"channel:user_id"` (ex: `whatsapp:55739...` ou `telegram:12345678`).
- **Canais Nativos Suportados:**
  - **WhatsApp:** Integração via WuzAPI para recebimento de áudios (transcritos com Whisper) e respostas em texto ou voz.
  - **Telegram:** Bot interativo para suporte técnico e comandos administrativos.
  - **Alexa Voice Skill:** Integração com AWS Lambda e canal sincronizado de resposta rápida com budget de timeout de 7 segundos.

### 🛡️ Política de Ferramentas Fail-Closed (`PolicyLevel`)
A execução de ferramentas por modelos de linguagem segue princípios de segurança estrita:
- Nenhuma ferramenta pode ser executada sem registro e homologação prévia no código.
- Cada ferramenta possui um nível de isolamento explícito:
  - `Global`: Ferramentas de leitura sem efeito colateral (cotações, status, consultas).
  - `Sandbox`: Ferramentas com escopo restrito e sanitização de argumentos.
  - `Restricted`: Requer autorização explícita ou chave com privilégios.
  - `Blocked`: Bloqueio imediato em tempo de execução.

### 🎙️ Pipeline de Voz Neural 24/7 & WhatsApp PTT
- **Zero Cost Voice Synthesis:** Utiliza síntese neural avançada rodando na VPS com latência inferior a 800ms para geração de fala humanizada sem custos por caractere.
- **Sanitização Fonética em Tempo de Execução:** Antes de sintetizar a fala, o texto é higienizado:
  - Remoção de emojis, tabelas e tags Markdown que soariam estranhos quando lidos por voz.
  - Conversão de abreviações e termos técnicos para formas de pronúncia natural em Português do Brasil.
- **Áudio Nativo (Push-To-Talk):** O arquivo de áudio é codificado no formato OGG com codec Opus e enviado com o header de áudio gravado nativamente, aparecendo com o microfone azul na interface do WhatsApp do destinatário.

### ⚡ Performance & Resiliência em Rust
- **Consumo Mínimo de Recursos:** Ocupa menos de 25MB de memória RAM residente, operando de forma estável 24/7 sem vazamentos de memória (memory leaks).
- **Sem Paradas por Garbage Collection:** Ideal para responder requisições de voz onde qualquer pausa de GC prejudicaria a experiência do usuário.
- **Daemon Nativo Linux:** Gerenciado diretamente pelo `systemctl`, iniciando automaticamente no boot do servidor e monitorado pelo watchdog `monitor-alphaclaw.sh`.

---

## 📁 Estrutura do Repositório

```text
alphaclaw/
├── src/
│   ├── main.rs               # Ponto de entrada e inicialização do runtime Tokio
│   ├── gateway/              # Abstração de canais de comunicação
│   │   ├── mod.rs            # Gateway/Channel traits e session keys
│   │   ├── telegram.rs       # Driver de transporte Telegram
│   │   ├── whatsapp.rs       # Driver WuzAPI / WhatsApp
│   │   └── alexa.rs          # Canal síncrono para Alexa Voice Skill
│   ├── agent/                # Loop cognitivo ReAct e orquestração
│   ├── tools/                # Registro e execução de ferramentas
│   │   ├── policy.rs         # Fail-closed security policy
│   │   └── builtins.rs       # Implementação das ferramentas homologadas
│   ├── search/               # Busca híbrida BM25 + embeddings vetoriais
│   └── selector.rs           # Roteamento inteligente de modelos de linguagem
├── Cargo.toml                # Dependências otimizadas para release musl
└── systemd/
    └── alphaclaw.service     # Definição do serviço Linux de produção
```

---

## ⚙️ Variáveis de Ambiente (`.env`)

```env
# Identidade & Gateway
RUST_LOG=info
GATEWAY_CHANNELS=whatsapp,telegram,alexa

# Provedores de LLM
GROQ_API_KEY=gsk_...
OPENAI_API_KEY=sk-...
ANTHROPIC_API_KEY=sk-ant-...

# Transcrição & Voz
WHISPER_PROVIDER=groq
VOICE_OUTPUT_ENGINE=edge-tts
VOICE_LANGUAGE=pt-BR-AntonioNeural

# Integrações de Mensageria
WUZAPI_URL=http://127.0.0.1:8081
WUZAPI_TOKEN=...
TELEGRAM_BOT_TOKEN=...
```
