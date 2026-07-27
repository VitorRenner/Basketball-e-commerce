# Roadmap do Projeto

Planejamento em sprints de 1 semana, pensado para execução individual em ritmo de estudo (paralelo à faculdade). Ajuste a duração conforme sua disponibilidade real.

## Visão geral das fases

```
Fase 1: Fundação        → Sprints 1-2
Fase 2: Catálogo         → Sprints 3-4
Fase 3: Carrinho/Pedido  → Sprints 5-6
Fase 4: Polimento        → Sprints 7-8
Fase 5: Deploy e extras  → Sprint 9+
```

---

## Sprint 1 — Setup e Fundação

**Objetivo:** ambiente rodando ponta a ponta, mesmo que vazio.

- [ ] Criar repositório Git, estrutura de pastas (backend/frontend)
- [ ] Configurar Django + DRF + PostgreSQL localmente
- [ ] Configurar projeto Vue 3 (Vite) + Pinia + Vue Router
- [ ] Configurar CORS entre backend e frontend
- [ ] Criar `.env.example` em ambos os projetos
- [ ] Primeiro commit com "Hello World" rodando nas duas pontas

## Sprint 2 — Autenticação

**Objetivo:** usuário consegue se cadastrar e logar.

- [ ] Model `User` customizado (ou extensão do padrão do Django)
- [ ] Endpoints de registro, login, refresh (`djangorestframework-simplejwt`)
- [ ] Telas de cadastro e login no frontend
- [ ] Store `auth` no Pinia (persistência de sessão)
- [ ] Rotas protegidas no Vue Router (`beforeEach` guard)
- [ ] Testes básicos de autenticação (backend)

## Sprint 3 — Catálogo (backend)

**Objetivo:** API de produtos e categorias funcionando.

- [ ] Models `Category` e `Product`
- [ ] Serializers e ViewSets (DRF)
- [ ] Filtros (categoria, busca, preço) e paginação
- [ ] Seed de dados fake (`Faker` ou fixtures) para testar com volume
- [ ] Documentação automática (drf-spectacular)

## Sprint 4 — Catálogo (frontend)

**Objetivo:** usuário navega pelo catálogo.

- [ ] Página de listagem de produtos (grid + paginação)
- [ ] Página de detalhe do produto
- [ ] Componente de filtro por categoria
- [ ] Campo de busca
- [ ] Estados de loading/erro/vazio

## Sprint 5 — Carrinho

**Objetivo:** usuário monta um carrinho, logado ou não.

- [ ] Model `Cart` e `CartItem` (backend)
- [ ] Endpoints de carrinho (add/update/remove)
- [ ] Store `cart` no Pinia (persistência local + sync com backend)
- [ ] Componente de carrinho (drawer ou página dedicada)
- [ ] Merge de carrinho anônimo → carrinho do usuário ao logar

## Sprint 6 — Checkout e Pedidos

**Objetivo:** fluxo de compra completo, do carrinho ao pedido confirmado.

- [ ] Models `Order` e `OrderItem`
- [ ] Lógica de checkout (decremento de estoque, snapshot de preço)
- [ ] Endpoint de checkout + listagem/detalhe de pedidos
- [ ] Fluxo de checkout no frontend (endereço → resumo → confirmação)
- [ ] Página de histórico de pedidos

## Sprint 7 — Painel Administrativo

**Objetivo:** lojista consegue gerenciar produtos e pedidos.

- [ ] Customizar Django Admin (list_display, filtros, busca)
- [ ] Upload de imagens de produto
- [ ] Gestão de status de pedidos
- [ ] Permissões (admin vs. cliente comum)

## Sprint 8 — Qualidade e Polimento

**Objetivo:** projeto robusto e apresentável.

- [ ] Cobertura de testes no backend (models, serializers, views críticas)
- [ ] Testes de componentes/stores críticos no frontend
- [ ] Tratamento de erros consistente (mensagens amigáveis)
- [ ] Responsividade mobile em todas as telas
- [ ] Revisão de UX (loading states, feedback visual, acessibilidade básica)
- [ ] README revisado com screenshots

## Sprint 9+ — Deploy e Extras

**Objetivo:** projeto no ar e com diferenciais.

- [ ] Deploy do backend (Render/Railway) + banco gerenciado
- [ ] Deploy do frontend (Vercel)
- [ ] Configurar CI básico (GitHub Actions: lint + testes a cada push)
- [ ] Domínio customizado (opcional)
- [ ] Extras conforme tempo disponível: cupom de desconto, avaliações de produto, integração de pagamento sandbox (Stripe/Mercado Pago), dashboard de métricas

---

## Marcos (milestones) sugeridos para o currículo

| Marco | O que já pode ser mostrado |
|---|---|
| Fim do Sprint 4 | Catálogo navegável, já dá pra printar telas |
| Fim do Sprint 6 | Fluxo de compra completo — MVP funcional |
| Fim do Sprint 8 | Projeto testado e polido — pronto para currículo |
| Fim do Sprint 9 | Link ao vivo, pronto para compartilhar em processos seletivos |

## Dica de ritmo

Não é necessário seguir a numeração de sprints à risca — o importante é **sempre ter algo funcionando de ponta a ponta** a cada etapa, mesmo que incompleto. Isso evita ficar semanas "no meio do caminho" sem nada demonstrável.
