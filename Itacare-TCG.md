# 🏪 Itacaré TCG

> **Marketplace multi-vendedor especializado em cartas colecionáveis e produtos de Pokémon TCG com checkout Mercado Pago, portal de lojistas e gestão de pedidos.**

[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![React](https://img.shields.io/badge/React-18.x-61DAFB?logo=react&logoColor=white)](https://reactjs.org/)
[![Node.js](https://img.shields.io/badge/Node.js-20_LTS-339933?logo=node.js&logoColor=white)](https://nodejs.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-47A248?logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![Mercado Pago](https://img.shields.io/badge/Mercado_Pago-Checkout_Pro-009EE3?logo=mercadopago&logoColor=white)](https://www.mercadopago.com.br/)
[![Status](https://img.shields.io/badge/Status-Em_Produção-brightgreen?style=flat-square)](#)

---

## 📖 Sobre o Projeto

O **Itacaré TCG** é uma plataforma de comércio eletrônico multi-vendedor desenvolvida sob medida para conectar colecionadores, jogadores e lojas de cartas colecionáveis (Pokémon TCG) na região litorânea da Bahia.

A plataforma soluciona a fragmentação de vendas em redes sociais (grupos de WhatsApp/Instagram), oferecendo um ambiente seguro com intermediação de pagamentos via Mercado Pago, verificação cadastral de vendedores, controle de estoque em tempo real e rastreamento de entregas.

---

## 🧱 Stack Tecnológica

| Camada | Tecnologias |
|---|---|
| **Frontend Web** | React 18, React Router DOM, Context API (Auth, Cart, Wishlist), TailwindCSS |
| **Backend API** | Node.js, Express, TypeScript, Mongoose (MongoDB 8) |
| **Gateway de Pagamento** | Mercado Pago SDK (Checkout Pro: PIX instantâneo, Cartão de Crédito e Boleto) + gerador local PIX |
| **Gestão de Mídia** | Cloudinary API (Upload direto de fotos das cartas com otimização webp e transformações on-the-fly) |
| **Email Transacional** | Brevo (Sendinblue) para confirmações de compras e atualizações de despacho |
| **Compliance & Validação** | Módulo de validação algorítmica de CPF/CNPJ e formatação tributária brasileira |

---

## 💎 Diferenciais Arquiteturais

### 🏬 Arquitetura Multi-Vendedor (Multi-Seller Marketplace)
- **Vitrine Unificada:** Clientes navegam por um catálogo centralizado com filtros por raridade, expansão, condição da carta (Near Mint, Lightly Played, etc.) e tipo.
- **Painel do Vendedor:** Lojistas e colecionadores possuem painel restrito para:
  - Cadastro de produtos com fotos reais de alta resolução via Cloudinary.
  - Controle de estoque unitário e precificação.
  - Acompanhamento de vendas e marcação de envio de encomendas.
- **Carrinho Inteligente:** Agrupamento de itens por vendedor com cálculo independente de taxas de entrega ou retiradas locais.

### 💳 Checkout Pro com Mercado Pago & Fallback Gracioso
- **Checkout Pro Integrado:** O fluxo de compra permite pagamento rápido via PIX (com aprovação em 2 segundos) e parcelamento no cartão.
- **Webhooks com Idempotência:** Processamento de webhooks do Mercado Pago que verifica o status real na API antes de liberar o pedido no banco, prevenindo confirmações duplicadas.
- **Degradação Graciosa (Graceful Degradation):** Em ambientes locais de teste ou caso credenciais externas sofram indisponibilidade pontual, o backend degrada graciosamente (logando ações sem interromper o boot do servidor).

### 🛠️ Painel Administrativo de Mediação
- Gestão centralizada de usuários, vendedores e status de aprovação de novos cadastros de lojistas.
- Relatórios de vendas por período e controle de taxas de plataforma.
- Painel de auditoria de pedidos para mediação rápida em caso de disputas.

---

## 📁 Estrutura do Repositório

```text
Itacare-TCG/
├── backend/
│   ├── index.ts              # Servidor Express com todas as rotas centralizadas
│   ├── auth.ts               # Autenticação JWT, sessões e middlewares de permissão
│   ├── models.ts             # Schemas: Seller, Product, User, Order, Notification, Settings
│   ├── payments.ts           # Orquestração de pagamentos e transições de status
│   ├── mercadopago.ts        # Integração oficial com Checkout Pro SDK
│   ├── pix.ts                # Payload e cálculo do QR Code PIX
│   ├── cpf.ts                # Validação de dígitos verificadores de CPF
│   └── cloudinary.ts         # Integração com storage de imagens
└── frontend/
    ├── src/
    │   ├── pages/            # 19 telas (Home, Catalog, ProductDetail, Cart, Checkout, Profile)
    │   ├── context/          # AuthContext, CartContext, WishlistContext
    │   ├── components/       # Navbar, Footer, ProductCard, FilterSidebar
    │   └── admin/            # Painel do Vendedor e Dashboard Administrativo da Plataforma
    └── vite.config.ts
```

---

## ⚙️ Variáveis de Ambiente (`backend/.env`)

```env
PORT=5000
NODE_ENV=production
MONGODB_URI=mongodb+srv://.../itacare_tcg_prod
JWT_SECRET=chave_secreta_jwt_longa_e_aleatoria

# Mercado Pago
MERCADOPAGO_ACCESS_TOKEN=APP_USR-...
MERCADOPAGO_PUBLIC_KEY=APP_USR-...

# Mídia & Email
CLOUDINARY_CLOUD_NAME=...
CLOUDINARY_API_KEY=...
CLOUDINARY_API_SECRET=...
BREVO_API_KEY=xkeysib-...
```
