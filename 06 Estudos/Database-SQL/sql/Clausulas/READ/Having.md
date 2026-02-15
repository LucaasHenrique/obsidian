***
**Criado em**: 2026-01-08  
**Modificado em**: 16:24
**Topico**: #sql
***
Permite filtra os resultados apos um `GROUP BY` ter sido aplicado

> A cláusula HAVING define restrições para as linhas retornadas por uma consulta que tiver GROUP BY

#Nota  -> Uma cláusula HAVING vem sempre imediatamente após uma cláusula GROUP BY. Sem uma cláusula GROUP BY, não pode haver cláusula HAVING. 

Essa consulta verifica o total de pedidos de cada usuario:
```sql
SELECT u.name, u.email, COUNT(o.id) FROM users u INNER JOIN orders o on o.user_id = u.id GROUP BY u.id;
``` 

Se quisermos exibir somente os clientes que fizeram exatamente 3 pedidos usamo `HAVING` para filtrar os dados agrupados:
```sql
SELECT u.name, u.email, COUNT(o.id) FROM users u INNER JOIN orders o on o.user_id = u.id GROUP BY u.id HAVING COUNT(o.id) = 3;
``` 
***
# HAVING X WHERE

Ambas são usadas para filtrar dados, porem são usadas em casos diferentes.

se quiser filtrar colunas especificas -> `WHERE`
se quiser filtrar agregações -> `HAVING`
***