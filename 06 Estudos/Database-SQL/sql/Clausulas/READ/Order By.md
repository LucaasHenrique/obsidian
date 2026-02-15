***
**Criado em**: 2026-01-08  
**Modificado em**: 16:43
**Topico**: #sql
***
Especifica como os dados de uma consulta devem ser classificados

> A consulta a seguir retorna uma lista de proprietários e cachoeiras, sem nenhuma classificação:
> 
>  `SELECT COALESCE(o.name, 'Unknown') AS owner, w.name AS waterfall_name FROM waterfall w LEFT JOIN owner o ON w.owner_id = o.id;` 

`COALESCE()` -> substitui todos os valores NULL  de uma coluna por um valor de sua preferencia.

> Neste caso, ela transformou os valores NULL da coluna o.name no texto Unknown. Se a função COALESCE não fosse usada aqui, todas as cachoeiras sem proprietários teriam sido deixadas de fora dos resultados. Em vez disso, agora elas estão marcadas como tendo um proprietário Unknown (desconhecido) e podem ser classificadas e incluídas nos resultados
***
```SQL
SELECT u.name, u.email, COUNT(o.id) AS PEDIDOS FROM users u INNER JOIN orders o on o.user_id = u.id GROUP BY u.id ORDER BY PEDIDOS ASC, name DESC;
```

Também podemos fazer a classificação usando colunas e expressões que não estão no select:
```SQL
SELECT u.name, u.email, COUNT(o.id) AS PEDIDOS FROM users u INNER JOIN orders o on o.user_id = u.id GROUP BY u.id ORDER BY o.id;
```
***
>Das seis cláusulas principais, só a cláusula ORDER BY não pode ser usada em uma subconsulta. Infelizmente, você não pode impor que as linhas de uma subconsulta sejam ordenadas. Para contornar esse problema, você teria de reescrever sua consulta com uma lógica diferente para evitar o uso de uma cláusula ORDER BY dentro da subconsulta e só a incluir na consulta externa. 

