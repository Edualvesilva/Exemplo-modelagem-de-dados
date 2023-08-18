# Comandos para operações CRUD no Banco de dados

## Resumo

- C -> CREATE (inserir dados usando comando `INSERT`)
- R -> READ (ler dados usando comando `SELECT`)
- U -> UPDATE (atualizar dados usando comando `UPDATE`)
- D -> DELETE (excluir dados usando comando `DELETE`)

## INSERT 

### Fabricantes

```sql
INSERT INTO fabricantes (nome) VALUES('Asus');

INSERT INTO fabricantes (nome) VALUES('Dell');

INSERT INTO fabricantes (nome) VALUES('Apple');

INSERT INTO fabricantes (nome) VALUES('LG'),('Samsung'),('Brastemp');

INSERT INTO fabricantes (nome) VALUES('Positivo'),('Microsoft');
```
### Produtos
```sql
INSERT INTO produtos(nome,preco,descricao,quantidade,fabricante_id)
 VALUES (
    'Ultrabook', 
    3500,
    'Equipamento de última geração cheio de recursos, com
    processador Intel Core i9 do balacobaco',
    7,
    2 -- id do fabricante DELL 
);

INSERT INTO produtos(nome,descricao,preco,quantidade,fabricante_id)
VALUES(
    'Tablet Android',
    'Tablet com a Versão 14 do sistema operacional android',
    1500.99,
    6,
    5
);

INSERT INTO produtos(nome,descricao,preco,quantidade,fabricante_id)
VALUES(
    'Geladeira',
    'Refrigerador Frost-free com acesso á internet',
    5200,
    12,
    6
);
INSERT INTO produtos(nome,descricao,preco,quantidade,fabricante_id)
VALUES(
    'Iphone 16',
    'Smartphone Apple cheio de frescuras e caro pra caramba',
    12666.66,
    3,
    3
),
 (
    'Ipad mini',
    'Tablet Apple com tela retina display',
    4999.01,
    5,
    3
);

INSERT INTO produtos (nome,descricao,preco,quantidade,fabricante_id)
VALUES(
    'Xbox Series S',
    'Velocidade e desempenho de última geração.',
    1997.00,
    5,
    8
),
(
    'Notebook Motion',
    'Intel Dual Core 4G de RAM,128GB SSD e Tela 14,1 Polegadas.',
    1213.65,
    8,
    7
);

```
---
## SELECT

```sql
SELECT * FROM produtos;

SELECT nome, preco FROM produtos;

SELECT preco,nome FROM produtos;

SELECT nome,preco,quantidade FROM produtos WHERE preco < 5000;

-- Mostre nome e descrição somente dos produtos da Apple
SELECT nome,descricao FROM produtos WHERE fabricante_id = 3;
```
### Operadores Lógicos: E,OU,NÃO

```sql
SELECT nome,preco FROM produtos WHERE preco >= 2000 AND preco <= 6000;

SELECT nome,preco FROM produtos WHERE preco > 5000 AND preco <= 6000;
```
### OU 

```sql
SELECT nome,preco FROM produtos WHERE preco > 5000 OR preco <= 6000;

-- Exiba nome e preco somente dos produtos 
-- da Apple e da Samsung

SELECT nome,preco FROM produtos WHERE fabricante_id IN(3,5);

SELECT nome,preco FROM produtos WHERE fabricante_id NOT IN(3,5);
```
#### NÃO
```sql
SELECT nome,descricao,preco FROM produtos WHERE NOT fabricante_id = 8;

-- versão usando operador racional "diferença/diferente" 
SELECT nome,descricao,preco FROM produtos WHERE  fabricante_id != 8;
```
---
## UPDATE

```sql
UPDATE fabricantes SET nome = 'Asus do Brasil' WHERE id = 1; -- NÃO SE ESQUEÇA DO WHERE!!!

-- UPDATE fabricantes2 SET nome = 'Asus do Paraguai';

UPDATE produtos SET preco = 6549.74 WHERE id = 4;

-- Altere a quantidade dos produtos da Apple e da Samsung para 20
UPDATE produtos SET quantidade = 20 WHERE fabricante_id IN(3,5);
```
## DELETE

```sql
DELETE FROM fabricantes WHERE id= 1;
DELETE FROM fabricantes WHERE id= 4;

-- A query abaixo NÃO FUNCIONA devido á restrição
-- de chave estrangeira/relacionamento, ou seja,
-- existem produtos associados ao fabricante 3 (apple)
-- DELETE FROM fabricantes WHERE id = 3;
```
---
## SELECT: outras formas de uso

### Classificando
```sql
SELECT nome,preco FROM produtos ORDER BY nome;
SELECT nome,preco FROM produtos ORDER BY preco;
SELECT nome,preco FROM produtos ORDER BY preco DESC;

-- DESC: classificação em ordem decrescente 
-- ASC(padrão): classificação em ordem crescente 

SELECT nome,preco FROM produtos WHERE quantidade = 20 ORDER BY nome;
```
### Busca de dados  

```sql
SELECT nome,descricao FROM produtos WHERE descricao LIKE "%sistema%" OR nome LIKE '%tela%';

-- Usamos o operador LIKE e o caractere coringa %
-- para permitir uma busca da palavra indicada em
-- qualquer posição dentro do texto. neste contexto,
-- o % significa 'qualquer texto' antes da palavra ou
-- depois da palavra.
```
### Operações e funções de agregação

```sql
SELECT SUM(preco) FROM produtos; -- SOMA
SELECT SUM(preco) as Total FROM produtos; -- alias/apelido

-- Exemplo de alias/apelido para outras colunas
SELECT nome as Produto,preco as "Preço" FROM produtos;

-- MÉDIA
SELECT AVG(preco) as "Média dos Preços" FROM produtos;
SELECT ROUND(AVG(preco),2) as "Média dos Preços" FROM produtos;

-- CONTAGEM
SELECT COUNT(id) as "Qtd de Produtos" FROM produtos;

SELECT COUNT(DISTINCT fabricante_id) as "Qtd de Fabricantes em produtos" FROM produtos;

-- DISTINCT é uma cláusula/flag que evita a duplicidade
-- na contagem de registros.
```
### Operações matemáticas

```sql
SELECT nome,preco,quantidade, (preco * quantidade) as Total FROM produtos;  
```
### Segmentação/Agrupamento de resultados

```sql
SELECT fabricante_id, SUM(preco) FROM produtos GROUP BY fabricante_id;
```

---
## Consultas (Queries) em duas ou mais tabelas relacionadas (JUNÇÃO/JOIN)
## Exibir nome do produto e nome do fabricante
```sql
-- SELECT tabela.coluna, tabela.coluna
SELECT produtos.nome as Produto, fabricantes.nome as Fabricante

--INNER JOIN é o comando que permite JUNTAR as tabelas
FROM produtos INNER JOIN fabricantes

-- ON comando para indicar a forma/critério da junção
ON produtos.fabricante_id = fabricantes.id;
```
### Nome do produto, nome do fabricante, ordenados pelo nome do produto

```sql
SELECT produtos.nome as Produto, fabricantes.nome as Fabricante
FROM produtos INNER JOIN fabricantes ON produtos.fabricante_id = fabricantes.id
ORDER BY Produto; -- ou produtos.nome
```
### Fabricante,soma dos preços e quantidade de produtos
```sql
SELECT fabricantes.nome as Fabricante,
SUM(produtos.preco) as Total, COUNT(produtos.fabricante_id) as "Qtd de produtos"
FROM produtos INNER JOIN fabricantes
ON produtos.fabricante_id = fabricantes.id
GROUP BY Fabricante
ORDER BY Total;
```
### Trazer a quantidade de produtos de cada fabricante e a soma da quantidade/estoque destes produtos, SOMENTE DOS FABRICANTES QUE POSSUEM PRODUTOS.

```sql
SELECT fabricantes.nome as Fabricante,COUNT(produtos.fabricante_id) as "Qtd de produtos",SUM(produtos.quantidade) as "Qtd em estoque"
FROM produtos INNER JOIN fabricantes
ON produtos.fabricante_id = fabricantes.id
GROUP BY Fabricante;
```
### Trazer a quantidade de produtos de cada fabricante e a soma da quantidade/estoque destes produtos,MESMO DOS FABRICANTES QUE POSSUEM PRODUTOS.
```sql
SELECT fabricantes.nome as Fabricante,COUNT(produtos.fabricante_id) as "Qtd de produtos",SUM(produtos.quantidade) as "Qtd em estoque"
FROM produtos RIGHT JOIN fabricantes
ON produtos.fabricante_id = fabricantes.id
GROUP BY Fabricante;

```

