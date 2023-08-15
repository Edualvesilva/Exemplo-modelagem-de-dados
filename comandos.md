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