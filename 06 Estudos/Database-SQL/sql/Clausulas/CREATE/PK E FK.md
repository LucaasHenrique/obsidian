---
id: PK E FK
aliases: []
tags: []
---
****
**Criado em**: 2026-01-09  
**Modificado em**: 21:31
**Topico**: #sql
***
# PRIMARY KEY

-> Uma `PRIMARY KEY` identifica de maneira exclusiva cada linha de dados  uma tabela. Ela pode ser composta por uma mais colunas da tabel. Toda tabela deve ter uma PK.

```sql
CREATE TABLE my_table (
	id INTEGER PRIMARY KEY,
	country VARCHAR(2),
	name VARCHAR(15)
);
```

varias colunas como PK:

```sql
CREATE TABLE my_table (
	id INTEGER PRIMARY KEY,
	country VARCHAR(2),
	name VARCHAR(15),
);
``` 

Uma `PRIMARY KEY`inclui as constraints `NOT NULL` e `UNIQUE`.
****
# FOREIGN KEY

->  Uma `FOREIGN KEY`de uma tabela é uma referencia a `PRIMARY KEY`de outra tabela. As duas tabelas podem ser vinculadas pela coluna em comum. Uma tabela pode ter zero ou mais `FOREIGN KEY`.

| Customers     |
| ------------- |
| id (pk)       |
| order_id (FK) |
| name          |
| location      |
|               |
   ↕

| Orders     |
| ---------- |
| o_id (PK)  |
| o_location |
| o_price    |
|            |
-> Na tabela customers sua coluna `order_id`apresenta correspondencia com os valores da coluna o_id, o que torna order_id uma `foreign key` pois referencia uma pk de outra tabela.

-> sql correspondente:

```sql
CREATE TABLE orders (
	o_id INTEGER PRIMARY KEY,
	o_location VARCHAR(20),
	o_price DECIMAL(6,2)
);
```

```sql
CREATE TABLE customers (
	id INTEGER PRIMARY KEY,
	order_id INTEGER,
	name VARCHAR(15),
	location VARCHAR(20),
	FOREIGN KEY (order_id)
	REFERENCES orders (o_id)
);
```

-> Em caso de dupla PK:

```sql
CREATE TABLE orders (
	o_id INTEGER,
	o_location VARCHAR(20),
	o_price DECIMAL(6,2),
	PRIMARY KEY (o_id, o_location)
);
```

```sql
CREATE TABLE customers (
	id INTEGER PRIMARY KEY,
	order_id INTEGER,
	name VARCHAR(15),
	location VARCHAR(20),
	CONSTRAINT fk_id_name
	FOREIGN KEY (order_id, location)
	REFERENCES orders (o_id, o_location)
);
