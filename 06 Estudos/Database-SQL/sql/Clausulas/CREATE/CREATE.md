****
**Criado em**: 2026-01-08  
**Modificado em**: 17:56
**Topico**: #
***
```SQL 
CREATE DATABASE my_db;
```
***
# CREATE EM TABELAS
```sql
CREATE TABLE my_simple_table (
	id INTEGER not null primary key,
	country VARCHAR(2),
	name VARCHAR(15)
);
``` 
***
# INSERINDO LINHAS
```sql
INSERT INTO my_simple_table(id, country, name) VALUES (1, 'BR', 'Maria');
``` 
***
# CRIANDO TABELA QUE NÃO EXISTE
->
```sql
CREATE TABLE IF NOT EXISTS my_simple_table (
	id INTEGER not null primary key,
	country VARCHAR(2),
	name VARCHAR(15)
);
``` 
***
# TABELA COM RESTRIÇÕES

-> Uma restrição é uma regra que especifica que dados podem ser inseridos em uma tabela:

```sql
CREATE TABLE another_table (
	country VARCHAR(2) NOT NULL, 
	name VARCHAR(15) NOT NULL,
	description VARCHAR(50),
	CONSTRAINT pk_another_table PRIMARY KEY (country, name)
);
``` 

```sql
CREATE TABLE my_table (
	id INTEGER NOT NULL,
	country VARCHAR(2) DEFAULT 'CA'
		CONSTRAINT chk_country CHECK (country IN ('CA', 'US')),
	name VARCHAR(15),
	cep_name VARCHAR(15),
	CONSTRAINT pk PRIMARY KEY (id),
	CONSTRIANT fk1 FOREING KEY (country, name) 
		REFERENCES another_table(country, name),
	CONSTRAINT unq_country_name UNIQUE (country, name),
	CONSTRAINT chk_upper_name CHECK (cap_name = UPPER(name))
);
```
***
read about [[PK E FK]]
read about [[Insert]]
