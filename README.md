# API de Gerenciamento de Tarefas

Uma API RESTful para gerenciamento de tarefas pessoais desenvolvida com Django e Django Rest Framework, com autenticação JWT.

## 🚀 Funcionalidades

- ✅ CRUD completo de tarefas
- 🔐 Autenticação JWT
- 👤 Gerenciamento de usuários
- 🔍 Filtros por status, data e prioridade
- 📝 Documentação Swagger/ReDoc
- 🔒 Proteção de dados por usuário

## 🛠️ Tecnologias Utilizadas

- Python 3.x
- Django 4.x
- Django Rest Framework
- SQLite
- JWT (JSON Web Tokens)
- drf-yasg (Swagger/ReDoc)

## 📋 Pré-requisitos

- Python 3.x
- pip (gerenciador de pacotes Python)
- Ambiente virtual (recomendado)

## ⚙️ Instalação

1. Clone o repositório:
   ```bash
   git clone https://github.com/seu-usuario/task-manager-api.git
   cd task-manager-api
   ```

2. Crie e ative um ambiente virtual:
   ```bash
   python -m venv venv
   .\venv\Scripts\activate
   ```

3. Execute as migrações:
   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

4. Crie um superusuário:
   ```bash
   python manage.py createsuperuser
   ```

5. Inicie o servidor:
   ```bash
   python manage.py runserver
   ```

## 📌 Endpoints

### Autenticação
- POST `/api/token/` - Obter token JWT
- POST `/api/token/refresh/` - Renovar token JWT

### Tarefas
- GET `/api/tasks/` - Listar tarefas
- POST `/api/tasks/` - Criar tarefa
- GET `/api/tasks/{id}/` - Detalhes da tarefa
- PUT `/api/tasks/{id}/` - Atualizar tarefa
- DELETE `/api/tasks/{id}/` - Deletar tarefa

### Documentação
- `/swagger/` - Documentação Swagger
- `/redoc/` - Documentação ReDoc

## 📝 Estrutura do Projeto

```
task_manager/
├── task_manager/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── tasks/
│   ├── migrations/
│   ├── __init__.py
│   ├── admin.py
│   ├── models.py
│   ├── serializers.py
│   └── views.py
└── manage.py
```

## 🔍 Exemplos de Uso

### Autenticação
```powershell
$body = @{
    username = "seu_usuario"
    password = "sua_senha"
} | ConvertTo-Json

Invoke-RestMethod -Method Post -Uri "http://localhost:8000/api/token/" -Body $body -ContentType "application/json"
```

### Criar uma Nova Tarefa
```powershell
$token = "seu_token_jwt"
$headers = @{
    "Authorization" = "Bearer $token"
    "Content-Type" = "application/json"
}

$novaTarefa = @{
    title = "Minha Tarefa"
    description = "Descrição da tarefa"
    due_date = "2024-03-30"
    priority = "ALTA"
} | ConvertTo-Json

Invoke-RestMethod -Method Post -Uri "http://localhost:8000/api/tasks/" -Headers $headers -Body $novaTarefa
```

### Listar Tarefas com Filtros
```powershell
# Filtrar por prioridade
Invoke-RestMethod -Method Get -Uri "http://localhost:8000/api/tasks/?priority=ALTA" -Headers $headers

# Filtrar tarefas completadas
Invoke-RestMethod -Method Get -Uri "http://localhost:8000/api/tasks/?completed=true" -Headers $headers

# Ordenar por data
Invoke-RestMethod -Method Get -Uri "http://localhost:8000/api/tasks/?ordering=due_date" -Headers $headers
```

## 📊 Modelo de Dados

### Task (Tarefa)
- `title`: CharField (max_length=200)
- `description`: TextField (opcional)
- `created_at`: DateTimeField (automático)
- `updated_at`: DateTimeField (automático)
- `due_date`: DateField
- `priority`: CharField (ALTA, MEDIA, BAIXA)
- `completed`: BooleanField
- `user`: ForeignKey (User)

## 🔐 Segurança

- Autenticação via JWT
- Cada usuário só pode ver e manipular suas próprias tarefas
- Tokens com expiração configurável
- Proteção contra CSRF
- Validação de dados via serializers

## 📖 Documentação da API

A documentação completa da API está disponível nas seguintes URLs:
- Swagger UI: `http://localhost:8000/swagger/`
- ReDoc: `http://localhost:8000/redoc/`