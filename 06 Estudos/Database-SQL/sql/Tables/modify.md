***
**Criado em**: 2026-02-06  
**Modificado em**: 06:39
**Topico**: #
***
-> modificação em tabelas é permanente!!!
***
### Renomeação
```sql
ALTER TABLE old_table_name RENAME TO new_table_name;
```

renomeação de coluna ->
```sql
ALTER TABLE my_table RENAME COLUMN old_table_name TO new_column_name;
``` 
***
### Add coluna
```sql
ALTER TABLE my_Table ADD new_column INTEGER;
```
***
## Exclusão de coluna
```sql
ALTER TABLE my_table DROP COLUMN new_column;
``` 
***
### Exibição, inclusão,modificação e exclusão de restrições
Uma restrição é uma regra que especifica que dados podem ser inseridos
em uma tabela.
MySQL -> 
```sql
SHOW CREATE TABLE my_table;
```
Postgresql ->
```shell
\d my_table
```
SQLite ->
```sql 
.schema table;
``` 
***
### Inclusão de uma constraint
- primeiro criamos uma table
```sql
CREATE TABLE my_table (
	id INTEGER NOT NULL,
	country VARCHAR(2) DEFAULT 'CA',
	name VARCHAR(15),
	lower_name VARCHAR(15)
);
``` 
Adicionamos uma constraint para que `lower_name` seja uma versão minuscula de `name`
Postgresql, MySQL, SQL server ->
```sql
ALTER TABLE my_table
	ADD CONSTRAINT chk_lower_name
	CHECK (lower_name = LOWER(name));
``` 
***
### Modificação de uma constraint
Postgresql
```sql
ALTER TABLE my_table
	ALTER country DROP DEFAULT,
	ALTER name TYPE VARCHAR(30);
```
MySQL
```sql
ALTER TABLE my_table
	MODIFY country VARCHAR(2) NULL,
	MODIFY name VARCHAR(30);
```
***
### Exclusão de uma constraint
```sql
ALTER TABLE my_table
	DROP CONSTRAINT chk_lower_name;
``` 