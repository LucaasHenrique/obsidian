***
**Criado em**: 2026-01-08  
**Modificado em**: 17:26
**Topico**: #sql
***
> Na visualização rápida de uma tabela, é prática recomendada retornar um número limitado de linhas em vez da tabela inteira.

Usada para retornar um numero limitado de dados na consulta select.

```SQL
SELECT u.name, u.email, COUNT(o.id) AS PEDIDOS FROM users u INNER JOIN orders o on o.user_id = u.id GROUP BY u.id ORDER BY PEDIDOS ASC, name DESC LIMIT 1;
```

-> retorna um somente uma linha na consulta.
