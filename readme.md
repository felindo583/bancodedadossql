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
    id_livro INT PRIMARY KEY AUTO_INCREMENT,
    titulo VARCHAR(150) NOT NULL,
    ano_publicacao YEAR,
    editora INT,
    autor INT,
    assunto INT,
    FOREIgn KEY(id_editora) REFERENCES editora(id_editora),
    FOREIgn KEY(id_autor) REFERENCES autor(id_autor),
    FOREIgn KEY(id_assunto) REFERENCES assunto(id_assunto)
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
...


## Passo 2: editar tabelas usando 'ALTER'
Apos a criação da tabela, podemos adcionar novos campos. Vamos adcionar uma coluna 'email' na tabela 'autor'

''''SQL
ALTER TABLE autor
ADD COLUMN email VARCHAR(100);
...

## Passo 3: Remover tabela usando 'DROP'
Se precisar de uma tabela usamos o comando drop

...
DROP TABLE extra
...

## Passo 4: Inserindo dados usando 'INSERT'
agora que as tabelas estão prontas, vamos inserir dados nelas.

#### Passo 4.1 Inserindo dados na tabela 'editora'
```SQL
INSERT INTO editora(nome_editora, pais)
VALUES
('editora alfa', 'brasil'),
('editora beta', 'portugal'),
('editora bertrand brasil', 'brasil');
```

#### 4.2 Inserindo dados na tabela 'autor'
'''SQL
INSERT INTO autor(nome_autor, data_nascimento, email)
VALUES 
('Jorge Amado','1912-08-10','jorginhoamado@email.com'),
('Machado de Assis','1839-06-21','machadinho@email.com'),
('Matt Haig','1975-06-03','matt@email.com');
'''
#### 4.3 Inserindo dados na tabela 'assunto'
''''SQL
INSERT INTO assunto (descricao_assunto)
VALUES
('Ficção'),
('Mistério'),
('Terror'),
('Romance');
''''

## Passo 5: atualizando os dados usando 'UPDATE'
Podemos atualizar os dados com o comando UPDATE.
Vamos corrir a data de publicação do livro 'capitaes da areia'

'''SQL
UPDATe livro
SET ano_publicacao = 1938
WHERe titulo = 'Capitaes da Areia';

'''

## Passo 6: Excluindo os dados usando 'DELETE'
Para remover os registros de uma tabela usamos o comando 'DELETE'.
Vamos excluir o livro 'memorias postumas de bras cubas'.

'''SQL
DELETE FROM livro
WHERE id_livro = 4;
'''
## Passo 7: Consultando os dados usando 'SELECT'
É possivel selecionar os dados para vizualizar da forma como quiser. Para isso usamos o comando 'SELECT'
#### Passo 7.1: selecionar todos os livros com suas editoras e autores
Vamos usar dados das tabelas 'livros', 'editora', 'autor', e 'assunto'
usando o comando 'JOIN'
'''SQL
SELECT livro.titulo AS nome,
       editora.nome_editora AS editora,
       autor.nome_autor AS autor,
       assunto.descricao_assunto AS tema,
       livro.ano_publicacao AS ano
FROM livro
JOIN editora ON livro.id_editora = editora.id_editora,
JOIN autor ON livro.id_autor = autor.id_autor,
JOIN assunto ON livro.id_assunto = assunto.id_assunto;
'''
#### Passo 7.2: selecionar todos os livros com o mesmo assunto
SELECT livro.titulo AS titulo,
       assunto.descricao_assunto AS tema
FROM livro
JOIN assunto ON livro.assunto = assunto.id_assunto
WHERE assunto.descricao_assunto = 'Romance';