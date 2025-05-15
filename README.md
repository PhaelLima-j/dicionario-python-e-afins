# 🐍 Dicionário Python e Afins

Repositório de consulta rápida para comandos, boas práticas e organização de projetos em Python.

---

## ✅ Ambiente Virtual com `venv` no VSCode

Para iniciar um projeto com ambiente virtual no VSCode utilizando o `venv`, primeiro crie o ambiente com o comando `python -m venv venv`. Em seguida, ative o ambiente virtual. No Windows (CMD), o comando é `venv\Scripts\activate`, no PowerShell é `.\venv\Scripts\Activate.ps1`, e no Linux ou macOS utilize `source venv/bin/activate`.

Depois de ativado, é possível instalar bibliotecas utilizando o pip. Se for instalar individualmente, use `pip install nome_da_biblioteca`. Caso o projeto já possua um arquivo `requirements.txt`, utilize `pip install -r requirements.txt` para instalar todas as dependências de uma vez.

Para rodar scripts Python, use `python nome_do_script.py`. Se o script estiver em uma subpasta, como por exemplo `api/script.py`, utilize `python api/script.py`.

É recomendado seguir uma estrutura organizada para o projeto. Um exemplo simples seria:

- A pasta `venv/` armazenando o ambiente virtual (que não deve ser versionada no Git);
- Um arquivo `requirements.txt` listando as dependências;
- Um arquivo `README.md` com a explicação do projeto;
- Um `.gitignore` configurado para ignorar o ambiente virtual;
- Um `main.py` como ponto de entrada do programa;
- E pastas para organizar funções, rotas ou outros módulos.

Para evitar que o ambiente virtual seja enviado ao repositório remoto, adicione `venv/` ao seu arquivo `.gitignore`.

Este repositório é pessoal, mas está aberto a contribuições e sugestões. Ele será atualizado constantemente conforme novas necessidades e experiências forem surgindo durante os projetos.


## ✅ Subindo um banco PostgreSQL no Docker

Rodar um banco de dados PostgreSQL localmente usando Docker, você pode utilizar o docker-compose. Abaixo, um exemplo básico de docker-compose.yml:

services:
 
    postgres:
 
        image: bitnami/postgresql:latest
 
        ports:
 
          - '5432:5433'
 
        environment:
 
          - POSTGRES_USER=postgres
 
          - POSTGRES_PASSWORD=senha
 
          - POSTGRES_DB=nome-banco
 
        volumes:
 
          - polls_pg_data:/bitnami/postgresql
 
   volumes:
 
    polls_pg_data:

### 🔍 Observações:
A porta externa é 5433 para evitar conflitos com instalações locais do PostgreSQL, mas você pode usar 5432:5432 se preferir.

A imagem da Bitnami já vem com boas práticas de segurança e configuração padrão.

O volume polls_pg_data garante que os dados do banco sejam persistidos mesmo que o container seja destruído.

O parâmetro restart: unless-stopped faz o container reiniciar automaticamente, exceto se você pará-lo manualmente.

### ▶️ Comandos úteis:

Para subir o serviço:
docker-compose up -d

Para parar os containers:
docker-compose down

Para verificar os logs:
docker-compose logs -f

Para acessar o banco via terminal:
docker exec -it postgres_container psql -U postgres1 -d sabesp_pathfinder

### 🧼 Dica de .gitignore:
Se estiver usando Docker e tiver volumes ou arquivos gerados localmente, adicione estas linhas ao seu .gitignore:

__pycache__/
*.pyc
.env
polls_pg_data/

## 🚀 Projeto FastAPI - API em Python

Este repositório contém a estrutura básica de uma aplicação FastAPI

---

### 📦 Tecnologias Utilizadas

- [FastAPI](https://fastapi.tiangolo.com/)
- [Uvicorn](https://www.uvicorn.org/)
- Python 3.8+

---

### ⚙️ Como executar o projeto

### 1. Clone o repositório

git clone https://github.com/seu-usuario/seu-repositorio.git
cd seu-repositorio
2. Crie um ambiente virtual (recomendado)

3. Instale as dependências

`pip install -r requirements.txt`
Caso o arquivo requirements.txt ainda não exista, instale diretamente:

`pip install fastapi uvicorn`
E depois:

`pip freeze > requirements.txt`

4. Estrutura do Projeto

 
       ├── app/
       │   ├── main.py             # Arquivo principal com a instância do FastAPI
       │   ├── routes/
       │   │   └── exemplo.py      # Exemplo de rota separada
       │   └── models/
       │       └── user.py         # Modelos com Pydantic
       ├── requirements.txt
       └── README.md
 
       
5. Execute o servidor

`uvicorn app.main:app --reload`
Acesse: http://localhost:8000

Documentação automática: http://localhost:8000/docs

Documentação alternativa: http://localhost:8000/redoc

### 📁 Exemplo de Código
main.py
python

```from fastapi import FastAPI
from app.routes import exemplo

app = FastAPI()

app.include_router(exemplo.router)

@app.get("/")
def read_root():
    return {"mensagem": "API FastAPI funcionando!"}
routes/exemplo.py

from fastapi import APIRouter

router = APIRouter()

@router.get("/exemplo")
def exemplo_rota():
    return {"rota": "exemplo"}
models/user.py

from pydantic import BaseModel

class User(BaseModel):
    id: int
    nome: str
    email: str
```
### ✅ Próximos Passos
🔗 Integrar com banco de dados (ex: SQLite, PostgreSQL) via SQLAlchemy ou Tortoise ORM

🧪 Adicionar testes com pytest e httpx

🔐 Implementar autenticação com OAuth2 ou JWT

⚙️ Gerenciar variáveis de ambiente com pydantic.BaseSettings ou python-dotenv

📚 Criar uma documentação completa da API com exemplos


