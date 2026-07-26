# Requisitos Funcionais e Não Funcionais

Este documento formaliza os requisitos do sistema, separados por camada (Backend, Frontend, Banco de Dados) e por tipo (Funcional / Não Funcional). Requisitos funcionais descrevem **o que o sistema faz**; não funcionais descrevem **como o sistema deve se comportar** (qualidade, performance, segurança).

Convenção de ID: `RF` = Requisito Funcional, `RNF` = Requisito Não Funcional.

---

## 1. Backend

### 1.1 Requisitos Funcionais — Backend

| ID | Descrição |
|---|---|
| RF-B01 | O sistema deve permitir cadastro de usuário com e-mail e senha |
| RF-B02 | O sistema deve autenticar usuários via JWT (access + refresh token) |
| RF-B03 | O sistema deve permitir que o usuário atualize seus dados de perfil |
| RF-B04 | O sistema deve permitir cadastro de múltiplos endereços por usuário |
| RF-B05 | O sistema deve expor endpoint de listagem de produtos com paginação |
| RF-B06 | O sistema deve permitir filtro de produtos por categoria, faixa de preço e busca textual |
| RF-B07 | O sistema deve expor endpoint de detalhe de produto por slug |
| RF-B08 | O sistema deve permitir adicionar, atualizar e remover itens de um carrinho |
| RF-B09 | O sistema deve suportar carrinho de usuário anônimo (via sessão) e migrá-lo ao carrinho do usuário no login |
| RF-B10 | O sistema deve validar disponibilidade de estoque antes de confirmar um pedido |
| RF-B11 | O sistema deve gerar um pedido a partir do carrinho no momento do checkout |
| RF-B12 | O sistema deve congelar (snapshot) nome e preço do produto no momento da compra |
| RF-B13 | O sistema deve decrementar o estoque do produto ao confirmar um pedido |
| RF-B14 | O sistema deve permitir consulta do histórico de pedidos do usuário logado |
| RF-B15 | O sistema deve permitir que um administrador altere o status de um pedido |
| RF-B16 | O sistema deve permitir CRUD de produtos e categorias via painel administrativo |
| RF-B17 | O sistema deve expor documentação interativa da API (Swagger/OpenAPI) |

### 1.2 Requisitos Não Funcionais — Backend

| ID | Descrição |
|---|---|
| RNF-B01 | A API deve responder em formato JSON, seguindo convenções REST |
| RNF-B02 | Senhas devem ser armazenadas com hash (nunca em texto puro) |
| RNF-B03 | Endpoints sensíveis (perfil, pedidos, checkout) devem exigir autenticação via token válido |
| RNF-B04 | A API deve responder listagens em até 500ms sob carga normal (ambiente de desenvolvimento) |
| RNF-B05 | O sistema deve ter cobertura de testes automatizados nas regras de negócio críticas (checkout, estoque, autenticação) |
| RNF-B06 | O código deve seguir um padrão de estilo consistente (PEP8 / linting automatizado) |
| RNF-B07 | Erros de validação devem retornar mensagens claras e códigos HTTP apropriados |
| RNF-B08 | CORS deve estar restrito ao domínio do frontend em produção |
| RNF-B09 | Variáveis sensíveis (secret key, credenciais de banco) não devem ser commitadas no repositório |
| RNF-B10 | A API deve ser versionável (ex: prefixo `/api/v1/`) para permitir evolução sem quebrar clientes existentes |

---

## 2. Frontend

### 2.1 Requisitos Funcionais — Frontend

| ID | Descrição |
|---|---|
| RF-F01 | O usuário deve poder se cadastrar e fazer login através de formulários dedicados |
| RF-F02 | O usuário deve poder navegar pelo catálogo de produtos com filtros e busca |
| RF-F03 | O usuário deve poder visualizar o detalhe de um produto, incluindo galeria de imagens |
| RF-F04 | O usuário deve poder adicionar, remover e alterar quantidade de itens no carrinho |
| RF-F05 | O carrinho deve ser visível e acessível a partir de qualquer página (ícone/badge) |
| RF-F06 | O usuário deve poder concluir o checkout selecionando endereço e revisando o pedido |
| RF-F07 | O usuário deve poder visualizar seu histórico de pedidos e o detalhe de cada um |
| RF-F08 | O sistema deve exibir mensagens de erro compreensíveis em caso de falha (ex: estoque insuficiente) |
| RF-F09 | O sistema deve exibir estados de carregamento (loading) durante requisições assíncronas |
| RF-F10 | Rotas que exigem autenticação devem redirecionar usuários não logados para a tela de login |

### 2.2 Requisitos Não Funcionais — Frontend

| ID | Descrição |
|---|---|
| RNF-F01 | A interface deve ser responsiva, funcionando corretamente em dispositivos mobile e desktop |
| RNF-F02 | O tempo de carregamento inicial da aplicação deve ser otimizado (lazy loading de rotas) |
| RNF-F03 | O estado da aplicação (carrinho, autenticação) deve ser gerenciado de forma centralizada (Pinia) |
| RNF-F04 | Componentes devem ser reutilizáveis e seguir um padrão de nomenclatura consistente |
| RNF-F05 | O carrinho de um usuário anônimo deve persistir entre recarregamentos de página (localStorage) |
| RNF-F06 | A aplicação deve ter cobertura de testes automatizados nos fluxos críticos (carrinho, checkout) |
| RNF-F07 | A aplicação deve seguir boas práticas básicas de acessibilidade (labels em formulários, contraste adequado) |
| RNF-F08 | Chamadas à API devem ser centralizadas em uma camada de serviço (não espalhadas nos componentes) |

---

## 3. Banco de Dados

### 3.1 Requisitos Funcionais — Banco de Dados

| ID | Descrição |
|---|---|
| RF-D01 | O banco deve armazenar usuários, endereços, categorias, produtos, imagens, carrinhos, itens de carrinho, pedidos e itens de pedido |
| RF-D02 | O banco deve suportar categorias hierárquicas (categoria pai/subcategoria) |
| RF-D03 | O banco deve permitir associar múltiplas imagens a um produto, com ordem de exibição |
| RF-D04 | O banco deve suportar carrinho vinculado a usuário autenticado ou a sessão anônima |
| RF-D05 | O banco deve preservar dados históricos do pedido (nome e preço do produto no momento da compra), independente de alterações futuras no produto |

### 3.2 Requisitos Não Funcionais — Banco de Dados

| ID | Descrição |
|---|---|
| RNF-D01 | O banco de dados deve ser relacional (PostgreSQL), garantindo integridade referencial entre pedidos, produtos e usuários |
| RNF-D02 | Campos únicos (e-mail de usuário, slug de produto/categoria) devem ter constraint de unicidade |
| RNF-D03 | Colunas usadas em filtros e buscas frequentes (slug, category_id, user_id) devem ter índice |
| RNF-D04 | Alterações de schema devem ser versionadas via migrations, nunca aplicadas manualmente em produção |
| RNF-D05 | Exclusão de produtos não deve remover fisicamente o registro caso existam pedidos associados (usar flag `is_active`) |
| RNF-D06 | O banco deve suportar transações atômicas no fluxo de checkout (criação do pedido + decremento de estoque não podem ocorrer parcialmente) |

---

## Rastreabilidade

Cada requisito funcional deste documento corresponde a um ou mais itens do [FUNCIONALIDADES.md](./FUNCIONALIDADES.md), e cada requisito não funcional reflete decisões já justificadas no [ARQUITETURA.md](./ARQUITETURA.md). Em caso de dúvida sobre a origem de um requisito, consultar esses documentos.
