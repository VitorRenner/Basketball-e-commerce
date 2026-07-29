DraftStoreEcommerce

Plataforma de e-commerce full stack desenvolvida como projeto de portfólio, com foco em demonstrar domínio de backend em Python (Django REST Framework) e frontend em Vue.js.

🚧 Status atual: planejamento e estruturação inicial. A documentação de requisitos, arquitetura e roadmap já está definida; a implementação do código está começando. Acompanhe o progresso pelo Roadmap.

🎯 Objetivo do projeto
Projeto criado para portfólio, demonstrando competências práticas para vagas de desenvolvedor(a) Jr, cobrindo todo o ciclo de desenvolvimento: modelagem de dados, API REST, consumo de API no frontend, autenticação, testes e deploy.

🛠️ Stack tecnológica

Backend

Python 3.12+

Django + Django REST Framework

PostgreSQL

JWT (autenticação)

pytest (testes)

Frontend

Vue 3 (Composition API)

Pinia (gerenciamento de estado)

Vue Router

Vitest (testes)

Axios

Infraestrutura

Docker / Docker Compose

GitHub Actions (CI)

Deploy: Render (backend) + Vercel (frontend)

📁 Estrutura do repositório

DraftStoreEcommerce/

├── docs/                  

# documentação de planejamento do projeto
│   ├── REQUISITOS.md                   # requisitos funcionais e não funcionais
│   ├── FUNCIONALIDADES.md              # features do MVP e extras, por módulo
│   ├── ARQUITETURA.md                  # decisões de arquitetura e fluxo de dados
│   ├── MODELAGEM_BD.md                 # schema do banco de dados e diagrama ER
│   ├── API.md                          # referência de endpoints da API REST
│   └── ROADMAP.md                      # plano de sprints
└── ecommerce/                           # código-fonte da aplicação
    ├── backend/                          # API em Django REST Framework
    └── frontend/                         # SPA em Vue 3
    
📚 Documentação completa

Documento	Conteúdo

REQUISITOS.md	Requisitos funcionais e não funcionais do sistema

FUNCIONALIDADES.md	Lista detalhada de features do MVP e extras

ARQUITETURA.md	Decisões de arquitetura, estrutura de pastas, fluxo de dados

MODELAGEM_BD.md	Schema do banco de dados e diagrama ER

API.md	Referência de endpoints da API REST

ROADMAP.md	Plano de sprints e cronograma de desenvolvimento

🚀 Como rodar o projeto localmente

Pré-requisitos

Python 3.12+

Node.js 20+

PostgreSQL 15+ (ou Docker)

Git

Backend

bash

# clonar o repositório

git clone https://github.com/VitorRenner/DraftStoreEcommerce.git

cd DraftStoreEcommerce/ecommerce/backend

# criar e ativar ambiente virtual

python -m venv venv

source venv/bin/activate  # Windows: venv\Scripts\activate

# instalar dependências

pip install -r requirements.txt

# configurar variáveis de ambiente

cp .env.example .env

# edite o .env com suas credenciais de banco

# rodar migrations

python manage.py migrate

# criar superusuário (acesso ao admin)

python manage.py createsuperuser

# rodar servidor de desenvolvimento

python manage.py runserver

Backend disponível em http://localhost:8000

Admin do Django em http://localhost:8000/admin

Documentação da API (Swagger) em http://localhost:8000/api/docs

Frontend

bash

cd DraftStoreEcommerce/ecommerce/frontend

# instalar dependências
npm install

# configurar variáveis de ambiente
cp .env.example .env

# rodar servidor de desenvolvimento
npm run dev

Frontend disponível em http://localhost:5173

Rodando com Docker (opcional)

bash

cd ecommerce

docker-compose up --build

🧪 Rodando os testes

bash

# backend

cd ecommerce/backend

pytest

# frontend

cd ecommerce/frontend

npm run test

🗺️ Roadmap

O desenvolvimento está organizado em sprints, cobrindo desde a modelagem inicial até deploy e testes. Veja o planejamento completo em docs/ROADMAP.md.
🌐 Deploy

Frontend (produção): a definir

Backend/API (produção): a definir

Documentação da API (produção): a definir

📝 Licença

Este é um projeto de portfólio, livre para fins de estudo e referência.

👤 Autor

Vitor Renner GitHub
