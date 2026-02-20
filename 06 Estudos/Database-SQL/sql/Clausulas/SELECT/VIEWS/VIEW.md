***
**Criado em**: 2026-02-11  
**Modificado em**: 06:39
**Topico**: #
***
Uma `view` é uma referencia aos dados resultantes de uma consulta sql.

é util para quando fazemos uma consulta SQL longa e complexa que contem muitas junções, filtros e agregações. Se os resultados da consulta são uteis provavelmente vamos querer referenciá-los novamente em algum momento 

Também é util para impedir que pessaos comuns tenham acesso ao banco de dados, o DBA pode criar uma view que mostre apenas o necessario ao usuario.
```sql
CREATE VIEW vw_users AS SELECT name, email, age FROM users;
```

```sql
SELECT * FROM vw_users;
```

Desse jeito podemos limitar dados sensiveis é mostrar somente o necessario.
***
```sql
SELECT o.id, o.name,
	COUNT(w.id) AS num_waterfalls
FROM owner o LEFT JOIN waterfall w
	ON o.id = w.owner_id
GROUP BY o.id, o.name;
``` 

se quissemos encontrar o media de `waterfalls`por owner, com uma view fariamos o seguinte:

-> criamos a view:
```sql
CREATE VIEW owner_waterfalls_vw AS
SELECT o.id, o.name, 
	COUNT(w.id) AS num_waterfalls
FROM owner o LEFT JOIN waterfall w
		ON o.id = w.owner_id
GROUP BY o.id, o.name; 
```

-> fazemos a consulta:
```sql
SELECT AVG(num_waterfalls) FROM owner_waterfalls
``` 
***

> Tanto as subconsultas quanto as views representam os resultados de uma 
>  consulta, que então também podem ser consultados. 
> • A subconsulta é temporária. Ela só existe pelo tempo de duração da consulta e é ótima para casos de execução única. 
> • A view é salva. Uma vez que uma view for criada, você poderá continuar escrevendo consultas que a referenciem.

