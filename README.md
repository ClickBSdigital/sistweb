# sistweb
 
 Criar as tabelas para o seu sistema, seguindo a lógica do projeto que envolve usuários, páginas e menus.

🗂️ Tabelas necessárias
usuarios - Armazena informações dos usuários.

paginas - Armazena as páginas disponíveis no sistema.

menu_usuario - Relaciona os menus com os usuários, definindo permissões.

-- 📌 Criando o Banco de Dados

CREATE DATABASE sistema_web;
USE sistema_web;

-- 1️⃣ Criando a tabela usuarios

CREATE TABLE usuarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL,
    senha VARCHAR(255) NOT NULL,
    tipo ENUM('admin', 'usuario') DEFAULT 'usuario',
    criado_em TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- 📌 Inserindo usuários de exemplo

INSERT INTO usuarios (nome, email, senha, tipo) VALUES
('Eliandro Silva', 'eliandro@email.com', '123456', 'admin'),
('Maria Souza', 'maria@email.com', 'senha123', 'usuario'),
('Carlos Mendes', 'carlos@email.com', 'segredo', 'usuario');


-- 2️⃣ Criando a tabela paginas

CREATE TABLE paginas (
    id INT AUTO_INCREMENT PRIMARY KEY,
    titulo VARCHAR(100) NOT NULL,
    conteudo TEXT NOT NULL,
    criada_em TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- 📌 Inserindo páginas de exemplo

INSERT INTO paginas (titulo, conteudo) VALUES
('Página Inicial', 'Bem-vindo ao nosso sistema.'),
('Sobre', 'Informações sobre a empresa.'),
('Contato', 'Entre em contato conosco.');

-- 3️⃣ Criando a tabela menu_usuario

CREATE TABLE menu_usuario (
    id INT AUTO_INCREMENT PRIMARY KEY,
    usuario_id INT NOT NULL,
    pagina_id INT NOT NULL,
    permitido BOOLEAN DEFAULT TRUE,
    FOREIGN KEY (usuario_id) REFERENCES usuarios(id) ON DELETE CASCADE,
    FOREIGN KEY (pagina_id) REFERENCES paginas(id) ON DELETE CASCADE
);

-- 📌 Inserindo permissões de menu

INSERT INTO menu_usuario (usuario_id, pagina_id, permitido) VALUES
(1, 1, TRUE),  -- Admin tem acesso à Página Inicial
(1, 2, TRUE),  -- Admin tem acesso à Sobre
(1, 3, TRUE),  -- Admin tem acesso ao Contato
(2, 1, TRUE),  -- Maria tem acesso à Página Inicial
(3, 1, TRUE);  -- Carlos tem acesso à Página Inicial

-- ✅ Banco de dados pronto!
Agora você pode utilizar essas tabelas no seu projeto PHP para autenticar usuários, exibir páginas e gerenciar permissões! 🚀


==========================================================================

O fluxo das pastas do seu projeto baseado no padrão MVC (Model-View-Controller) pode seguir esta estrutura:


/meu_projeto
│── /app
│   │── /Controllers
│   │   ├── UsuarioController.php
│   │   ├── PaginasController.php
│   │── /Models
│   │   ├
│   │   ├── Paginas.php
│   │── /Views
│   │   ├── /layouts
│   │   │   ├── header.php
│   │   │   ├── footer.php
│   │   ├── /usuarios
│   │   │   ├── index_user.php
│   │   │   ├── create_user.php
│   │   │   ├── edit_user.php
│   │   │   ├── delete_user.php
│   │   ├── /paginas
│   │   │   ├── home.php
│   │   │   ├── about.php
│   │   │   ├── contact.php
│── /config
│   │── Database.php
│── /public
│   │── index.php
│   │── /css
│   │── /js
│── /routes
│   │── web.php
│── .htaccess
│── composer.json
│── README.md


📂 Explicação:
app/Controllers/ → Contém os arquivos que controlam as requisições e interagem com os modelos e as views.

app/Models/ → Representa as tabelas do banco de dados, com classes que manipulam os dados.

app/Views/ → Contém os arquivos de interface do usuário. Dentro dela, temos subpastas para organizar os arquivos de diferentes entidades.

config/Database.php → Gerencia a conexão com o banco de dados.

public/ → Contém os arquivos acessíveis ao usuário final, como imagens, scripts JS e folhas de estilo CSS.

routes/web.php → Define as rotas do sistema.

.htaccess → Configuração para direcionamento correto das URLs no Apache.

composer.json → Arquivo de configuração do Composer caso use dependências externas.

README.md → Documentação do projeto.

Esse fluxo organiza bem o projeto seguindo MVC e facilita manutenção e escalabilidade.