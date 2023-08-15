 # Comandos SQL - Referências

## Modelagem Física com comandos DDL

### Criar banco de dados

CREATE DATABASE vendas CHARACTER SET utf8mb4;

### Criar tabela de fabricantes

```sql
CREATE TABLE fabricantes(
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(45) NOT NULL
); 
```
### Visualizar detalhes estruturais da tabela

```sql
DESC fabricantes;
```
### Criar tabela de produtos
```sql
CREATE TABLE produtos (
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(45) NOT NULL,
    descricao TEXT(400) NULL,
    preco DECIMAL(6,2) NOT NULL,
    fabricante_id INT NOT NULL 
);
```

### Criação do relacionamento entre as tabelas (chave estrangeira)
```sql
ALTER TABLE produtos
    -- CONSTRAINT/RESTRIÇÃO indicando o nome do relacionamento
    ADD CONSTRAINT fk_produtos_fabricantes

    -- Criando a chave-estrangeira (fabricante_id) que
    -- aponta para a chave-primária (id) de outra tabela (fabricantes)
    FOREIGN KEY (fabricante_id) REFERENCES fabricantes(id);
```

### Exemplos de alteração estruturais na tabela

#### Renomear tabela

```sql
ALTER TABLE fabricantes RENAME TO fornecedores;
```
#### Modificar colunas

```sql
ALTER TABLE produtos 
MODIFY COLUMN preco INT NOT NULL;
```
#### Renomear colunas

```sql
ALTER TABLE fabricantes
    CHANGE nome nome_do_fabricante VARCHAR(20) NOT NULL;

ALTER TABLE fabricantes
    CHANGE nome_do_fabricante nome VARCHAR(45) NOT NULL;
```
#### Adicionar coluna
```sql
ALTER TABLE produtos 
    ADD quantidade INT NULL AFTER preco;
```

# Exercício de Modelagem

No phpMyAdmin utilize comandos SQL para fazer a modelagem física do exercício anterior.
Você deve:

Criar um novo banco de dados (Catálogo de Filmes)
Criar duas tabelas (Gêneros e Filmes)
Fazer o relacionamento entre as tabelas

## Criando novo banco de dados
```sql
CREATE DATABASE catalogo_filmes CHARACTER SET utf8mb4;
```
### Criando Tabelas
```sql
CREATE TABLE generos(
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(45)
);

CREATE TABLE FILMES (
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    titulo VARCHAR(45),
    ano YEAR,
    generos_id INT NOT NULL
);

ALTER TABLE FILMES RENAME TO filmes;

ALTER TABLE filmes
    ADD CONSTRAINT fk_filmes_generos
    FOREIGN KEY (generos_id) REFERENCES generos(id);
```