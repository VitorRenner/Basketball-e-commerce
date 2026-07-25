# E-commerce — Projeto de Portfólio

Plataforma de e-commerce full stack desenvolvida como projeto de portfólio, com foco em demonstrar domínio de backend em Python (Django REST Framework) e frontend em Vue.js.

## 🎯 Objetivo do projeto

Projeto criado para portfólio, com o objetivo de demonstrar competências práticas para vagas de desenvolvedor(a) Jr, cobrindo todo o ciclo de desenvolvimento: modelagem de dados, API REST, consumo de API no frontend, autenticação, testes e deploy.

## 🛠️ Stack tecnológica

**Backend**
- Python 3.12+
- Django + Django REST Framework
- PostgreSQL
- JWT (autenticação)
- pytest (testes)

**Frontend**
- Vue 3 (Composition API)
- Pinia (gerenciamento de estado)
- Vue Router
- Vitest (testes)
- Axios

**Infraestrutura**
- Docker / Docker Compose
- GitHub Actions (CI)
- Deploy: Render (backend) + Vercel (frontend)

## 📁 Documentação completa

| Documento | Conteúdo |
|---|---|
| [FUNCIONALIDADES.md](./FUNCIONALIDADES.md) | Lista detalhada de features do MVP e extras |
| [ARQUITETURA.md](./ARQUITETURA.md) | Decisões de arquitetura, estrutura de pastas, fluxo de dados |
| [MODELAGEM_BD.md](./MODELAGEM_BD.md) | Schema do banco de dados e diagrama ER |
| [API.md](./API.md) | Referência de endpoints da API REST |
| [ROADMAP.md](./ROADMAP.md) | Plano de sprints e cronograma de desenvolvimento |

## 🚀 Como rodar o projeto localmente

### Pré-requisitos
- Python 3.12+
- Node.js 20+
- PostgreSQL 15+ (ou Docker)
- Git

### Backend

```bash
# clonar o repositório
git clone https://github.com/seu-usuario/ecommerce-portfolio.git
cd ecommerce-portfolio/backend

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
```

Backend disponível em `http://localhost:8000`
Admin do Django em `http://localhost:8000/admin`
Documentação da API (Swagger) em `http://localhost:8000/api/docs`

### Frontend

```bash
cd ecommerce-portfolio/frontend

# instalar dependências
npm install

# configurar variáveis de ambiente
cp .env.example .env

# rodar servidor de desenvolvimento
npm run dev
```

Frontend disponível em `http://localhost:5173`

### Rodando com Docker (opcional)

```bash
docker-compose up --build
```

## 🧪 Rodando os testes

```bash
# backend
cd backend
pytest

# frontend
cd frontend
npm run test
```

## 🌐 Deploy

- **Frontend (produção):** [link a definir]
- **Backend/API (produção):** [link a definir]
- **Documentação da API (produção):** [link a definir]

## 📸 Screenshots

_A adicionar após implementação das telas principais._

## 📝 Licença

Este é um projeto de portfólio, livre para fins de estudo e referência.

## 👤 Autor

**Vitor** — Estudante de Engenharia de Software
[LinkedIn] · [GitHub]
