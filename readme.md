# passo a passo: Criação de um banco de dados
Tutorial de como criar um banco de dados sql que organiza as infor,ações de 'livros', 'editora', 'autores e assuntos'.
Este guia sera dividido em etapas para demonstrar desde a criação de tabelas, chaves e ate manipulação/ consulta de dados.

# resumo de uma estrutura sql
*__CREATE__ para criar 'banco de dados' ou 'tabelas'
*__ALTER__ para adcionar ou modficar colunas 
*__DROP__ para remover 'banco de dados' ou 'tabelas'
*__INSERT__ para adcionar registros na tabela
*__UPDATE__ para atualizar os registros
*__DELETE__ para remover os registros
*__SELECT__ para consultar e vizualizar dados

## passo 1: criação do Banco de Dados e das Tabelas
#### 1.1 Criando o DB

...

CREATE DATABASE biblioteca;
USE biblioteca;

#### 1.2 Criando tabela 'Editora'

...

CREATE TABLE editora (
    id_editora INT PRIMARY KEY AUTO_INCREMENT,
    nome_editora VARCHAR(100) NOT NULL,
    pais VARCHAR(50)
);

#### 1.3 Criando a tabela 'autor'
...

CREATE TABLE autor(
    id_autor INT PRIMARY KEY AUTO_INCREMENT,
    nome_autor VARCHAR(200),
    data_nascimento DATE
);
...

#### 1.4 Criando a tabela 'assunto'
...

CREATE TABLE assunto (
    id_assunto INT PRIMARY KEY AUTO_INCREMENT,
    descricao_assunto VARCHAR(300) NOT NULL
);

#### 1.5 Criando a tabela 'livro'
...

CREATE TABLE livro(
    id_livro INT PRIMARY KEY AUTO_INCREMENT
    titulo VARCHAR(150) NOT NULL,
    ano_publicacao YEAR,
    FOREING KEY(id_editora), REFERENCES editora(id_editora),
    FOREING KEY(id_autor) REFERENCES autor(id_autor),
    FOREING KEY(id_assunto) REFERENCE assunto
    (id_assunto)
);
...

#### 1.6 Criando uma tabela EXTRA
A tabela EXTRA vai servir para exemplificar a exclusão

...

CREATE TABLE extra(
    id INT PRIMARY KEY AUTO_INCREMENT,
    produtos VARCHAR(50),
    quantidade INT(20),
    preco DOUBLE NOT NULL
);