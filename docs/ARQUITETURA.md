# Arquitetura do Sistema

## Visão geral

O sistema segue uma arquitetura **desacoplada (decoupled)**, com backend expondo uma API REST e frontend consumindo essa API via HTTP. Essa separação permite que os dois times/camadas evoluam de forma independente e é o padrão mais comum no mercado atualmente.

```
┌─────────────────┐         HTTPS/REST        ┌──────────────────┐
│                  │  ────────────────────>    │                  │
│  Frontend (Vue)  │                            │  Backend (DRF)   │
│                  │  <────────────────────    │                  │
└─────────────────┘         JSON               └──────────────────┘
                                                          │
                                                          │ ORM
                                                          ▼
                                                 ┌──────────────────┐
                                                 │   PostgreSQL     │
                                                 └──────────────────┘
```

## Decisões de arquitetura

### Por que Django REST Framework?

- Admin panel pronto reduz tempo de desenvolvimento de um painel de gestão do zero
- ORM maduro, com migrations e proteção contra SQL injection nativa
- Sistema de autenticação e permissões já testado em produção por milhares de projetos
- Ecossistema robusto (drf-spectacular para docs, django-cors-headers, djangorestframework-simplejwt)

### Por que Vue 3 + Composition API?

- Curva de aprendizado mais suave que React, mantendo reatividade poderosa
- Composition API favorece reuso de lógica (composables) e organização por funcionalidade
- Pinia como state manager é simples e com boa integração com TypeScript (se adotado futuramente)

### Por que separar backend e frontend (ao invés de Django Templates)?

- Reflete o padrão real de mercado (SPA + API REST)
- Permite deploy independente (frontend em CDN/Vercel, backend em servidor próprio)
- Facilita futura expansão para app mobile consumindo a mesma API

## Estrutura de pastas — Backend

```
backend/
├── core/                   # configurações do projeto Django
│   ├── settings/
│   │   ├── base.py
│   │   ├── dev.py
│   │   └── prod.py
│   ├── urls.py
│   └── wsgi.py
├── apps/
│   ├── users/              # autenticação, perfil
│   │   ├── models.py
│   │   ├── serializers.py
│   │   ├── views.py
│   │   └── urls.py
│   ├── products/           # catálogo, categorias
│   ├── cart/                # carrinho
│   ├── orders/              # pedidos, checkout
│   └── common/               # utilitários compartilhados
├── tests/
├── requirements.txt
├── manage.py
└── .env.example
```

## Estrutura de pastas — Frontend

```
frontend/
├── src/
│   ├── assets/
│   ├── components/         # componentes reutilizáveis (Button, Card, etc.)
│   ├── views/               # páginas (ProductList, ProductDetail, Cart, Checkout...)
│   ├── stores/               # Pinia stores (auth, cart, products)
│   ├── router/                # Vue Router
│   ├── services/               # camada de comunicação com a API (axios)
│   ├── composables/             # lógica reutilizável (useAuth, useCart...)
│   └── App.vue
├── tests/
├── package.json
└── .env.example
```

## Fluxo de autenticação

1. Usuário faz login → backend retorna `access_token` (curta duração) e `refresh_token` (longa duração)
2. Frontend armazena tokens (em memória + refresh token em cookie httpOnly, idealmente)
3. Requisições subsequentes enviam `access_token` no header `Authorization: Bearer <token>`
4. Quando `access_token` expira, frontend usa `refresh_token` para obter um novo, de forma transparente (interceptor do Axios)

## Fluxo de dados: adicionar produto ao carrinho (exemplo)

1. Usuário clica em "Adicionar ao carrinho" na `ProductDetail.vue`
2. Componente chama a action `addToCart` da `cartStore` (Pinia)
3. Se usuário não está logado → carrinho é persistido no `localStorage`
4. Se usuário está logado → store dispara requisição `POST /api/cart/items/` para o backend
5. Backend valida estoque disponível, associa item ao carrinho do usuário, retorna carrinho atualizado
6. Store atualiza o estado local, componentes reativos (ícone do carrinho, badge de quantidade) atualizam automaticamente

## Comunicação entre camadas

- Toda comunicação frontend ↔ backend acontece via **API REST** (JSON), documentada em [API.md](./API.md)
- CORS configurado no backend para aceitar apenas o domínio do frontend em produção
- Variáveis sensíveis (secret keys, credenciais de banco) nunca commitadas — uso de `.env` + `.env.example` como referência

## Ambiente e deploy

| Camada | Desenvolvimento | Produção |
|---|---|---|
| Backend | `localhost:8000` | Render / Railway |
| Frontend | `localhost:5173` | Vercel |
| Banco de dados | PostgreSQL local (Docker) | PostgreSQL gerenciado (Render/Railway/Neon) |

## Possíveis evoluções futuras

- Cache de queries pesadas com Redis
- Fila assíncrona (Celery) para envio de e-mails e processamento de pagamento
- Containerização completa com Docker Compose para dev e produção
