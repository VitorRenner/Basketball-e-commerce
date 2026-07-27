# Documentação da API

Base URL (desenvolvimento): `http://localhost:8000/api/`

Todas as respostas são em formato JSON. Endpoints protegidos exigem o header:
```
Authorization: Bearer <access_token>
```

Documentação interativa (Swagger/OpenAPI) disponível em `/api/docs` quando o servidor estiver rodando.

---

## Autenticação

| Método | Endpoint | Descrição | Autenticação |
|---|---|---|---|
| POST | `/auth/register/` | Cria novo usuário | Não |
| POST | `/auth/login/` | Retorna access + refresh token | Não |
| POST | `/auth/refresh/` | Renova o access token | Não (usa refresh token) |
| POST | `/auth/logout/` | Invalida o refresh token | Sim |

**Exemplo — POST `/auth/login/`**

Request:
```json
{
  "email": "usuario@email.com",
  "password": "senha123"
}
```

Response `200`:
```json
{
  "access": "eyJhbGciOiJIUzI1NiIs...",
  "refresh": "eyJhbGciOiJIUzI1NiIs...",
  "user": {
    "id": 1,
    "email": "usuario@email.com",
    "first_name": "Vitor"
  }
}
```

---

## Usuários

| Método | Endpoint | Descrição | Autenticação |
|---|---|---|---|
| GET | `/users/me/` | Retorna dados do usuário logado | Sim |
| PATCH | `/users/me/` | Atualiza perfil do usuário logado | Sim |
| GET | `/users/me/addresses/` | Lista endereços do usuário | Sim |
| POST | `/users/me/addresses/` | Cria novo endereço | Sim |
| PATCH | `/users/me/addresses/{id}/` | Edita endereço | Sim |
| DELETE | `/users/me/addresses/{id}/` | Remove endereço | Sim |

---

## Produtos e Categorias

| Método | Endpoint | Descrição | Autenticação |
|---|---|---|---|
| GET | `/categories/` | Lista todas as categorias | Não |
| GET | `/products/` | Lista produtos (paginado) | Não |
| GET | `/products/{slug}/` | Detalhe de um produto | Não |

**Query params suportados em `GET /products/`**

| Parâmetro | Exemplo | Descrição |
|---|---|---|
| `category` | `?category=eletronicos` | Filtra por slug da categoria |
| `search` | `?search=tenis` | Busca textual por nome |
| `min_price` / `max_price` | `?min_price=50&max_price=200` | Filtro de faixa de preço |
| `ordering` | `?ordering=-created_at` | Ordenação (`price`, `-price`, `-created_at`) |
| `page` | `?page=2` | Paginação |

**Exemplo — GET `/products/tenis-esportivo/`**

Response `200`:
```json
{
  "id": 12,
  "name": "Tênis Esportivo Runner",
  "slug": "tenis-esportivo",
  "description": "Tênis leve para corrida...",
  "price": "199.90",
  "stock_quantity": 15,
  "category": {
    "id": 3,
    "name": "Calçados",
    "slug": "calcados"
  },
  "images": [
    { "id": 1, "image_url": "https://.../img1.jpg", "order": 0 }
  ]
}
```

---

## Carrinho

| Método | Endpoint | Descrição | Autenticação |
|---|---|---|---|
| GET | `/cart/` | Retorna o carrinho atual | Opcional* |
| POST | `/cart/items/` | Adiciona item ao carrinho | Opcional* |
| PATCH | `/cart/items/{id}/` | Atualiza quantidade de um item | Opcional* |
| DELETE | `/cart/items/{id}/` | Remove item do carrinho | Opcional* |

*Carrinho de visitante usa `session_key` (cookie); carrinho de usuário logado usa `user_id`. Ao logar, o carrinho da sessão é mesclado ao carrinho do usuário.

**Exemplo — POST `/cart/items/`**

Request:
```json
{
  "product_id": 12,
  "quantity": 2
}
```

Response `201`:
```json
{
  "id": 5,
  "items": [
    {
      "id": 8,
      "product": { "id": 12, "name": "Tênis Esportivo Runner", "price": "199.90" },
      "quantity": 2,
      "subtotal": "399.80"
    }
  ],
  "total": "399.80"
}
```

---

## Pedidos e Checkout

| Método | Endpoint | Descrição | Autenticação |
|---|---|---|---|
| POST | `/orders/checkout/` | Finaliza o pedido a partir do carrinho | Sim |
| GET | `/orders/` | Lista pedidos do usuário logado | Sim |
| GET | `/orders/{id}/` | Detalhe de um pedido | Sim |
| PATCH | `/orders/{id}/cancel/` | Cancela um pedido (se status permitir) | Sim |

**Exemplo — POST `/orders/checkout/`**

Request:
```json
{
  "address_id": 3,
  "payment_method": "simulated"
}
```

Response `201`:
```json
{
  "id": 45,
  "status": "pending",
  "subtotal": "399.80",
  "shipping_cost": "20.00",
  "total": "419.80",
  "items": [
    { "product_name_snapshot": "Tênis Esportivo Runner", "unit_price_snapshot": "199.90", "quantity": 2 }
  ],
  "created_at": "2026-07-24T14:30:00Z"
}
```

---

## Painel administrativo (uso interno)

Gerenciado majoritariamente via Django Admin (`/admin/`), sem necessidade de endpoints REST dedicados no MVP. Caso o dashboard customizado (item stretch) seja implementado, os endpoints abaixo serão adicionados:

| Método | Endpoint | Descrição | Autenticação |
|---|---|---|---|
| PATCH | `/orders/{id}/status/` | Atualiza status de um pedido | Sim (admin) |
| GET | `/admin/metrics/` | Métricas de vendas | Sim (admin) |

---

## Códigos de status HTTP utilizados

| Código | Significado |
|---|---|
| 200 | Sucesso |
| 201 | Recurso criado |
| 204 | Sucesso sem conteúdo (ex: delete) |
| 400 | Erro de validação |
| 401 | Não autenticado |
| 403 | Autenticado, mas sem permissão |
| 404 | Recurso não encontrado |
| 409 | Conflito (ex: estoque insuficiente) |

## Formato de erro padrão

```json
{
  "detail": "Estoque insuficiente para o produto solicitado.",
  "code": "insufficient_stock"
}
```
