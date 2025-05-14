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
 
          - POSTGRES_USER=postgres1
 
          - POSTGRES_PASSWORD=Optz@tech2025
 
          - POSTGRES_DB=sabesp_pathfinder
 
        volumes:
 
          - polls_pg_data:/bitnami/postgresql
 
volumes:
 
    polls_pg_data:

###🔍 Observações:
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

