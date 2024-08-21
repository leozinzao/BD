-- 1. Criação do Banco de Dados
-- Este comando cria um novo banco de dados chamado "Bookstore" e depois começa a usá-lo.
CREATE DATABASE Bookstore;
USE Bookstore;

-- 2. Criação das Tabelas

-- Tabela Fornecedor
-- Cria uma tabela chamada "Fornecedor" que guarda informações sobre fornecedores (nome, CNPJ, contato).
CREATE TABLE Fornecedor (
    ID_Fornecedor INT AUTO_INCREMENT PRIMARY KEY, -- Chave primária que identifica cada fornecedor de forma única
    Nome VARCHAR(100) NOT NULL, -- Nome do fornecedor
    CNPJ VARCHAR(14) NOT NULL UNIQUE, -- CNPJ, campo único
    Contato VARCHAR(50) -- Informação de contato do fornecedor
);

-- Tabela Livro
-- Cria uma tabela chamada "Livro" para armazenar os dados dos livros (título, autor, preço, quantidade em estoque).
CREATE TABLE Livro (
    ID_Livro INT AUTO_INCREMENT PRIMARY KEY, -- Chave primária que identifica cada livro de forma única
    Título VARCHAR(150) NOT NULL, -- Título do livro
    Autor VARCHAR(100), -- Autor do livro
    Preço DECIMAL(10, 2) NOT NULL, -- Preço do livro com até 2 casas decimais
    Quantidade_Estoque INT NOT NULL, -- Quantidade de livros disponíveis em estoque
    ID_Fornecedor INT, -- Relaciona o livro com o fornecedor usando uma chave estrangeira
    FOREIGN KEY (ID_Fornecedor) REFERENCES Fornecedor(ID_Fornecedor) -- Configura a chave estrangeira que aponta para a tabela Fornecedor
);

-- Tabela Cliente
-- Cria uma tabela chamada "Cliente" para guardar informações dos clientes (nome, email, telefone).
CREATE TABLE Cliente (
    ID_Cliente INT AUTO_INCREMENT PRIMARY KEY, -- Chave primária que identifica cada cliente de forma única
    Nome VARCHAR(100) NOT NULL, -- Nome do cliente
    Email VARCHAR(100) NOT NULL UNIQUE, -- Email do cliente, campo único
    Telefone VARCHAR(20) -- Telefone do cliente
);

-- Tabela Venda
-- Armazena as vendas realizadas, associando-as a um cliente.
CREATE TABLE Venda (
    ID_Venda INT AUTO_INCREMENT PRIMARY KEY, -- Chave primária que identifica cada venda
    Data DATE NOT NULL, -- Data da venda
    ID_Cliente INT, -- Relaciona a venda a um cliente usando uma chave estrangeira
    Total DECIMAL(10, 2) NOT NULL, -- Total da venda
    FOREIGN KEY (ID_Cliente) REFERENCES Cliente(ID_Cliente) -- Configura a chave estrangeira que aponta para a tabela Cliente
);

-- Tabela Item_Venda
-- Armazena os itens vendidos em cada venda, relacionando o livro à venda.
CREATE TABLE Item_Venda (
    ID_Item INT AUTO_INCREMENT PRIMARY KEY, -- Chave primária que identifica cada item de venda
    ID_Venda INT, -- Relaciona o item a uma venda usando uma chave estrangeira
    ID_Livro INT, -- Relaciona o item a um livro usando uma chave estrangeira
    Quantidade INT NOT NULL, -- Quantidade de livros vendidos
    Preço DECIMAL(10, 2) NOT NULL, -- Preço do livro na venda
    FOREIGN KEY (ID_Venda) REFERENCES Venda(ID_Venda), -- Configura a chave estrangeira que aponta para a tabela Venda
    FOREIGN KEY (ID_Livro) REFERENCES Livro(ID_Livro) -- Configura a chave estrangeira que aponta para a tabela Livro
);

-- 3. Inserção de Dados Fictícios

-- Insere dados fictícios na tabela Fornecedor.
INSERT INTO Fornecedor (Nome, CNPJ, Contato) VALUES
('Editora ABC', '12345678000195', 'contato@editoraabc.com'),
('Editora XYZ', '98765432000198', 'info@editoraxyz.com');

-- Insere dados fictícios na tabela Livro.
INSERT INTO Livro (Título, Autor, Preço, Quantidade_Estoque, ID_Fornecedor) VALUES
('O Grande Livro', 'Autor A', 49.90, 10, 1),
('Outro Livro', 'Autor B', 29.90, 20, 2);

-- Insere dados fictícios na tabela Cliente.
INSERT INTO Cliente (Nome, Email, Telefone) VALUES
('Maria Silva', 'maria.silva@example.com', '1234-5678'),
('João Pereira', 'joao.pereira@example.com', '8765-4321');

-- Insere dados fictícios na tabela Venda.
INSERT INTO Venda (Data, ID_Cliente, Total) VALUES
('2024-08-20', 1, 79.80),
('2024-08-21', 2, 29.90);

-- Insere dados fictícios na tabela Item_Venda.
INSERT INTO Item_Venda (ID_Venda, ID_Livro, Quantidade, Preço) VALUES
(1, 1, 1, 49.90),
(1, 2, 1, 29.90),
(2, 2, 1, 29.90);

-- 4. Consulta Simples

-- Esta consulta traz uma lista das vendas realizadas por cliente, mostrando nome do cliente, data da venda, o livro vendido, a quantidade e o preço.
SELECT 
    c.Nome AS Cliente, -- Nome do cliente
    v.Data AS Data_Venda, -- Data da venda
    l.Título AS Livro, -- Título do livro
    iv.Quantidade, -- Quantidade de livros vendidos
    iv.Preço -- Preço do livro na venda
FROM 
    Cliente c
JOIN 
    Venda v ON c.ID_Cliente = v.ID_Cliente -- Junta as tabelas Cliente e Venda
JOIN 
    Item_Venda iv ON v.ID_Venda = iv.ID_Venda -- Junta as tabelas Venda e Item_Venda
JOIN 
    Livro l ON iv.ID_Livro = l.ID_Livro -- Junta as tabelas Item_Venda e Livro
ORDER BY 
    c.Nome, v.Data; -- Ordena o resultado pelo nome do cliente e pela data da venda
