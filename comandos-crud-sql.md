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
