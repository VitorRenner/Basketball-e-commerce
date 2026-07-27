# Funcionalidades

Este documento detalha todas as funcionalidades do sistema, organizadas por módulo e por prioridade (MVP vs. Extras).

## Legenda de prioridade

- 🟥 **MVP** — essencial, sem isso o projeto não está completo
- 🟨 **Extra** — diferencial, implementar após o MVP estar estável
- 🟩 **Stretch** — "se sobrar tempo", bom para mostrar ambição

---

## 1. Autenticação e Usuários

| Funcionalidade | Prioridade | Descrição |
|---|---|---|
| Cadastro de usuário | 🟥 MVP | Nome, e-mail, senha (com confirmação e validação de força) |
| Login | 🟥 MVP | Autenticação via JWT (access + refresh token) |
| Logout | 🟥 MVP | Invalidação/descarte do token no client |
| Recuperação de senha | 🟨 Extra | Fluxo de "esqueci minha senha" via e-mail |
| Edição de perfil | 🟥 MVP | Nome, e-mail, telefone, endereços salvos |
| Múltiplos endereços | 🟨 Extra | Usuário pode salvar mais de um endereço de entrega |
| Login social (Google) | 🟩 Stretch | OAuth2 com Google |

## 2. Catálogo de Produtos

| Funcionalidade | Prioridade | Descrição |
|---|---|---|
| Listagem de produtos | 🟥 MVP | Grid paginado com imagem, nome, preço |
| Página de detalhe do produto | 🟥 MVP | Descrição completa, galeria de imagens, variações (se houver) |
| Busca por nome | 🟥 MVP | Busca textual simples |
| Filtro por categoria | 🟥 MVP | Navegação por categorias/subcategorias |
| Filtro por faixa de preço | 🟨 Extra | Slider de min/max |
| Ordenação (preço, relevância, novidade) | 🟨 Extra | Dropdown de ordenação |
| Avaliações e notas de produtos | 🟩 Stretch | Usuários avaliam produtos comprados |
| Produtos relacionados | 🟩 Stretch | "Quem viu este também viu" |

## 3. Carrinho de Compras

| Funcionalidade | Prioridade | Descrição |
|---|---|---|
| Adicionar produto ao carrinho | 🟥 MVP | Com seleção de quantidade |
| Remover produto do carrinho | 🟥 MVP | — |
| Alterar quantidade | 🟥 MVP | Atualização em tempo real do subtotal |
| Persistência do carrinho (visitante) | 🟥 MVP | localStorage para usuário não logado |
| Persistência do carrinho (logado) | 🟨 Extra | Sincroniza carrinho com backend ao logar |
| Cálculo de frete | 🟨 Extra | Simulado ou integração com API de frete (ex: Melhor Envio) |
| Cupom de desconto | 🟩 Stretch | Aplicação de código promocional |

## 4. Checkout e Pedidos

| Funcionalidade | Prioridade | Descrição |
|---|---|---|
| Resumo do pedido | 🟥 MVP | Itens, quantidades, subtotal, frete, total |
| Seleção/cadastro de endereço de entrega | 🟥 MVP | — |
| Pagamento simulado | 🟥 MVP | Fluxo de checkout que gera o pedido, sem gateway real |
| Integração de pagamento real (sandbox) | 🟨 Extra | Stripe ou Mercado Pago em modo sandbox |
| Confirmação de pedido por e-mail | 🟨 Extra | E-mail transacional simples |
| Histórico de pedidos do usuário | 🟥 MVP | Lista de pedidos com status |
| Detalhe do pedido | 🟥 MVP | Itens, status, valor, endereço usado |
| Cancelamento de pedido | 🟨 Extra | Usuário pode cancelar pedido em status inicial |

## 5. Painel Administrativo

| Funcionalidade | Prioridade | Descrição |
|---|---|---|
| CRUD de produtos | 🟥 MVP | Via Django Admin customizado |
| CRUD de categorias | 🟥 MVP | — |
| Gestão de estoque | 🟥 MVP | Quantidade disponível por produto |
| Gestão de pedidos (mudar status) | 🟥 MVP | Ex: pendente → pago → enviado → entregue |
| Dashboard com métricas básicas | 🟩 Stretch | Total de vendas, produtos mais vendidos |
| Upload de múltiplas imagens por produto | 🟨 Extra | — |

## 6. Qualidade e Infraestrutura (transversal)

| Funcionalidade | Prioridade | Descrição |
|---|---|---|
| Testes automatizados (backend) | 🟥 MVP | pytest cobrindo models, serializers e views principais |
| Testes automatizados (frontend) | 🟨 Extra | Vitest cobrindo componentes e stores críticos |
| Documentação da API (Swagger) | 🟥 MVP | drf-spectacular |
| Tratamento de erros e validações | 🟥 MVP | Mensagens de erro claras no frontend |
| Responsividade (mobile-first) | 🟥 MVP | Layout funcional em mobile e desktop |
| CI básico (lint + testes) | 🟨 Extra | GitHub Actions |
| Deploy em produção | 🟥 MVP | Backend + frontend acessíveis publicamente |
| Rate limiting na API | 🟩 Stretch | Proteção básica contra abuso |

---

## Critério de "pronto para o currículo"

O projeto pode ser considerado apresentável quando **todos os itens 🟥 MVP** estiverem implementados, testados e em deploy funcional. Os itens 🟨 e 🟩 são incrementos para destacar o projeto depois disso.
