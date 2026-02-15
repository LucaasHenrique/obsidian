***
**Criado em**: 2026-01-06  
**Modificado em**: 18:17
**Topico**: #sql
***
Por padrão com quando utlizamos uma *Select* todas linhas são retornadas, mesmo havendo duplicatas.

Se quiseres remover as duplicatas durante uma consulta basta utilizar a clausula **DISTINCT**:

```sql
SELECT DISTINCT user_id FROM orders;
```

- independente se o usuario fez 500 pedidos, ele só será exibido na consulta uma vez.
***
# COUNT e DISTINCT

Para contar o número de valores exclusivos existentes dentro de uma única coluna, você pode combinar as palavras-chave COUNT e DISTINCT dentro da cláusula SELECT.

```sql
SELECT COUNT(DISTINCT type) FROM owner;
```

```sql
SELECT COUNT(DISTINCT user_id) from orders;
```

- para contar o numero de combinções exclusivas de varias colunas voce pode inserir uma consulta DISTINCT como uma subconsulta e então fazer a contagem na subconsulta.

```sql
SELECT COUNT(*) AS num_unique FROM (SELECT DISTINCT o.type, w.open_to_public FROM owner o JOIN waterfall w ON o.id = w.owner_id) my_subquery;
```

Equivalente em postgresql ou MySQL:
```sql
SELECT COUNT(DISTINCT oi.quantity, p.name)
AS num_unique
FROM order_items oi JOIN products p
ON oi.product_id = p.id;
```
***






