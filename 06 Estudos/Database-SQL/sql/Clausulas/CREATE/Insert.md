***
**Criado em**: 2026-02-05  
**Modificado em**: 06:58
**Topico**: #
***
## Inserção dos resultados de uma consulta em uma tabela

em vez de digitar os valores manualmente, você pode carregar uma nova tabela com os dados de tabelas existentes.

```sql
SELECT * FROM my_simple_table;
```
 
criando uma nova tabela ->

```sql
CREATE TABLE new_table_two_columns (
	id INTEGER,
	name VARCHAR(15)
);
```

inserindo os dados da consulta na nova tabela.

```SQL
INSERT INTO new_table_two_columns (id, name)
	SELECT id, name 
	FROM my_simple_table
WHERE id < 3; 
```
***
### Também podemos inserir valores de uma tabela existente e adicionar ou modificar outros valores durante o processo.

new table -> 
``` sql
CREATE TABLE new_table_four_columns ( 
	id INTEGER, name VARCHAR(15), 
	new_num_column INTEGER, 
	new_text_column VARCHAR(30) 
);
```

inserindo os valores da consulta

```sql
INSERT INTO new_table_four_columns (id, name, new_num_column, new_text_column)
	SELECT id, name, 2017, 'stargazing'
	FROM my_simple_table
WHERE id = 2;
```

inserindo valores da consulta e alterando algum valor

```sql
INSERT INTO new_table_four_columns
(id, name, new_num_column, new_text_column)
	SELECT 3, name, 2017, 'wolves'
	FROM my_simple_table
WHERE id = 2;
```
***
## Podemos inserir dados de um arquivo de texto, como .csv, no bd

![[Pasted image 20260205072213.png]]

criamos uma nova tabela

``` sql
CREATE TABLE new_table (
	id INTEGER,
	country VARCHAR(2),
	name VARCHAR(15)
);
```

No PostgreSQL

```sql
\copy new_table
FROM '<file_path>/my_data.csv'
DELIMITER ',' CSV HEADER
```
***
118