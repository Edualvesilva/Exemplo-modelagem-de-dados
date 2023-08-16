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







```


