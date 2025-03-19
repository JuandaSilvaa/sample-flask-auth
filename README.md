# 🔐 Autenticação de Usuários com Flask

Este projeto foi desenvolvido durante o módulo de **Desenvolvimento Avançado com Flask** da Rocketseat. Ele implementa um sistema de **autenticação de usuários** utilizando **Flask**, **Flask-Login** e **SQLAlchemy**, além de contar com suporte a **Docker** para facilitar a configuração do ambiente. O sistema permite a criação, autenticação, atualização e remoção de usuários, garantindo que apenas usuários autorizados possam acessar determinados recursos.

## 📌 Funcionalidades

- 🔑 **Autenticação de usuários** com Flask-Login
- 📝 **Cadastro de novos usuários**
- 🔍 **Recuperação de dados de um usuário**
- ✏️ **Atualização de credenciais**
- 🗑 **Deleção de usuários** (apenas por administradores)
- 🔐 **Proteção de rotas** (usuários precisam estar logados para acessar certos recursos)

## 🚀 Tecnologias Utilizadas

- Python 3.13.2
- Flask
- Flask-Login (gerenciamento de sessão do usuário)
- SQLAlchemy (ORM para interação com o banco de dados)
- Bcrypt (para hash de senhas)
- Docker e Docker Compose (para facilitar a configuração do ambiente)

## 📂 Estrutura do Projeto

```
sample-flask-auth/
├─ instance/
│  └─ database.db
├─ models/
│  └─ user.py
├─ .gitignore
├─ app.py
├─ database.py
├─ docker-compose.yml
├─ README.md
└─ requirements.txt
```

## 📝 Como Executar o Projeto

1. **Clone o repositório**:

   ```bash
   git clone https://github.com/seuusuario/sample-flask-auth.git
   ```

2. **Navegue até a pasta do projeto**:

   ```bash
   cd sample-flask-auth
   ```

3. **Instale as dependências**:

   ```bash
   pip install -r requirements.txt
   ```

4. **Execute a aplicação**:

   ```bash
   python app.py
   ```

   Isso iniciará o servidor na URL `http://127.0.0.1:5000/`.

## 🔄 Rotas da API

### 🔑 Autenticação

- `POST /login` → Autentica um usuário
- `GET /logout` → Realiza logout do usuário autenticado

### 📝 Usuários

- `POST /user` → Cria um novo usuário
- `GET /user/<id>` → Obtém informações de um usuário
- `PUT /user/<id>` → Atualiza senha de um usuário (somente o próprio usuário ou admin)
- `DELETE /user/<id>` → Deleta um usuário (somente administradores)

## ⚠️ Regras de Acesso

- Apenas **administradores** podem **deletar outros usuários**.
- Usuários podem **atualizar apenas a própria senha**.
- Apenas **usuários autenticados** podem acessar as rotas protegidas.

## 🐳 Executando com Docker

Se preferir, você pode rodar o projeto via **Docker**:

1. **Verifique e ajuste o arquivo `docker-compose.yml`**:

   O projeto já inclui um serviço de banco de dados MySQL configurado no Docker Compose:

   ```yaml
   services:
     db:
       image: mysql:latest
       restart: always
       environment:
         MYSQL_USER: 'admin'
         MYSQL_PASSWORD: 'admin123'
         MYSQL_DATABASE: 'flask-crud'
         MYSQL_ROOT_PASSWORD: 'admin123'
       ports:
         - "3306:3306"
       expose:
         - '3306'
       volumes:
         - /seu/diretorio/personalizado/mysql:/var/lib/mysql
   ```

   **Atenção**: Você deve alterar o caminho do volume (`/seu/diretorio/personalizado/mysql`) para um diretório adequado em sua máquina.

2. **Construa e suba os containers**:

   ```bash
   docker-compose up --build
   ```

3. O servidor será iniciado em `http://127.0.0.1:5000/`.

**Nota**: Esta configuração é apenas para testes.

