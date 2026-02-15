***
**Criado em**: 2026-02-06  
**Modificado em**: 07:19
**Topico**: #
***
### Update em colunas
```SQL
UPDATE my_table SET name = LOWER(name);
```

### Update em linhas
```sql
UPDATE products SET stock = stock - 2 WHERE id = 2;
```

importante sempre usar where para evitar q as atualizações se propaguem para todos os dados!!!
***
### Atualização delinhas de dados comos resultados de uma consulta
primeiro visualize a alteração desejada com um `select`.

é depois faça:
```sql
UPDATE my_table
	SET awards = (SELECT MIN(awards) FROM my_table)
	WHERE country = 'CA';
```
*** 