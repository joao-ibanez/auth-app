# Auth App - Gerenciador de Posts e Categorias

Uma aplicação web desenvolvida com o framework **Laravel 12**, utilizando **PHP 8.2+** e o pacote **Laravel Breeze** para autenticação e controle de acesso, além de **Tailwind CSS** e **Vite** no frontend.

---

## 🚀 Funcionalidades

### 🔐 Autenticação e Perfil (Laravel Breeze)
- Cadastro de novos usuários.
- Login e Logout com segurança.
- Recuperação de senha por e-mail.
- Painel de controle (`/dashboard`) protegido por autenticação.
- Gerenciamento de dados do perfil e exclusão de conta.

### 📂 Categorias (CRUD)
- Listagem, criação, edição e exclusão de categorias.
- Proteção de acesso: apenas usuários autenticados podem gerenciar categorias.

### 📝 Posts (CRUD com Imagem)
- Criação de posts com título, texto, imagem de capa e vínculo a uma categoria.
- Validação automática de formulários (tamanho e tipo de imagem).
- Upload e remoção automática de imagens no servidor usando o sistema de armazenamento (`Storage`) do Laravel.
- Listagem e gerenciamento de publicações de forma organizada.

---

## 🛠️ Stack Tecnológica

- **Backend:** Laravel 12 (PHP >= 8.2)
- **Autenticação:** Laravel Breeze (Blade / Tailwind)
- **Frontend:** HTML5, CSS3, Tailwind CSS, Blade Templates
- **Build Tool:** Vite
- **Banco de Dados:** MySQL / PostgreSQL / SQLite (configurável no `.env`)

---

## ⚙️ Instalação e Execução

### Passo 1: Clonar o projeto e acessar a pasta
```bash
git clone https://github.com/joao-ibanez/auth-app.git
cd auth-app
```

### Passo 2: Executar o Setup Automático
O projeto já conta com um script automatizado no Composer que instala dependências, copia o `.env`, gera a chave da aplicação, roda as migrations e compila o frontend:
```bash
composer setup
```

*(Caso não tenha executado as migrations com banco configurado, lembre-se de configurar o arquivo `.env` com suas credenciais de banco de dados e rodar `php artisan migrate`.)*

### Passo 3: Criar o link simbólico para as imagens
Para permitir a exibição correta das imagens enviadas nos posts:
```bash
php artisan storage:link
```

### Passo 4: Rodar o servidor de desenvolvimento
Execute o comando abaixo para iniciar simultaneamente o servidor Laravel, o Vite (frontend) e as filas de processamento:
```bash
composer dev
```

A aplicação estará disponível em: [http://localhost:8000](http://localhost:8000)

---

## 📁 Estrutura de Rotas Principal

| Método | URI | Ação | Nome da Rota | Protegida? |
|---|---|---|---|---|
| `GET` | `/` | Exibe a página welcome | `welcome` | Não |
| `GET` | `/dashboard` | Painel administrativo básico | `dashboard` | Sim (auth, verified) |
| `GET/POST/...` | `/categorias` | CRUD de Categorias | `categorias.*` | Sim (auth) |
| `GET/POST/...` | `/posts` | CRUD de Posts | `posts.*` | Sim (auth) |
| `GET/POST/...` | `/profile` | Gerenciamento de Perfil | `profile.*` | Sim (auth) |
