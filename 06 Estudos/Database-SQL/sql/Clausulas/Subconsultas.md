***
**Criado em**: 2026-01-06  
**Modificado em**: 17:55
**Topico**: #sql
***
subconsults não correlacionadas versus correlacionadas:

Não correlacionadas: 
```sql
SELECT id, name, population, (SELECT AVG(population) FROM county) AS average_pop FROM county;
```
- O exemplo anterior é uma  subconsulta não correlacionada, o que significa que a subconsulta não referencia a consulta externa.
- funciona sozinha, independenete da query externa
- é executada somente uma vez.
- "Calcule a média da população **uma vez** e mostre esse valor em todas as linhas.”

Correlacionada:
```sql
SELECT o.id, o.name,
       (SELECT COUNT(*)
        FROM waterfall w
        WHERE o.id = w.owner_id) AS num_waterfalls
FROM owner o;
```
 
- Ja uma subconsulta correlacionada é aquela que referencia valores da consultaa externa
- A subconsulta utiliza a valor o.id da consulta externa, criando uma correlação
- "Para **cada owner**, conte quantas waterfalls pertencem a ele."
****
🛑 Por questoões de performance sempre é melhor reescrever uma subconsulta correlacionada com joins:
``` sql
SELECT o.id, o.name, COUNT(w.id) AS num_waterfalls
	FROM owner o
	LEFT JOIN waterfall w ON o.id = w.owner_id
GROUP BY o.id, o.name;
```
***
As subconsultas existentes dentro da cláusula FROM devem ser instruções SELECT autônomas, o que significa que elas não referenciarão a consulta externa e poderão ser executadas de maneira independente.

uma subconsulta tambem pode ser chamada de tabela porque acaba agindo como uma tabela pelo tempo que durar a consulta.

```sql
SELECT w.name AS waterfall_name, o.name AS owner_name
FROM waterfall w
JOIN owner o ON w.owner_id = o.id
WHERE o.type = 'public'
ORDER BY waterfall_name;
```
***
## Subconsultas versus a cláusula WITH

Uma alternativa à criação de uma subconsulta seria a criação de uma CTE (common table expression, expressão de tabela comum) com o uso de uma cláusula WITH

- A principal vantagem é que a subconsulta é inserida logo no inicio do codigo, gerando um sql mais limpo e também permite referenciar a subconsulta várias vezes.

```sql
WITH o AS (SELECT * FROM owner WHERE type = 'public') SELECT w.name AS waterfall_name, o.name AS owner_name FROM o JOIN waterfall w ON o.id = w.owner_id;
```

```sql
WITH o AS (SELECT * FROM order_items WHERE quantity > 1) 
SELECT p.name AS 'product name', o.quantity AS 'quantity' FROM o INNER JOIN products p on p.id = o.product_id;  
```
***
## Por que usar uma subconsulta na cláusula FROM
Utilizando subconsults podemos transformar um problema maior  em problemas menores: 

Exemplo 1: Várias etapas para a obtenção dos resultados.
- Suponhamos que você quisesse encontrar a média das paradas feitas em um passeio. Primeiro, precisaria encontrar o número de paradas de cada passeio e, em seguida, calcular a média dos resultados. A consulta a seguir encontra o número de paradas de cada passeio: 
```sql
SELECT name, MAX(stop) as num_stops FROM tour GROUP BY name;
```

- Poderíamos então transformar a consulta em uma subconsulta e escrever outra consulta externa a ela para encontrar a média

```sql
SELECT AVG(num_stops) FROM (SELECT name, MAX(stop) as num_stops FROM tour GROUP BY name) tour_stops;
``` 
***
Exemplo 2: A tabela da cláusula FROM é muito grande
O objetivo original seria listarmos todas as cachoeiras públicas. Isso pode ser feito sem uma subconsulta e com uma JOIN:

```sql
SELECT w.name AS waterfall_name, o.name AS owner_name FROM
owner o INNER JOIN waterfall w ON o.id = w.owner_id WHERE o.type = 'public';
```

🛑 Casos as tabelas sejam muito grandes a junção pode ser demorada, para otimizar podemos utilizar uma subconsulta ja que estamos interessados somente nas cachoeiras publicas. Então depois fazer a junção:

```SQL
SELECT w.name AS waterfall_name, o.name AS owner_name FROM (SELECT * FROM owner WHERE type = 'public') o JOIN waterfall w on w.owner_id = o.id;
```
***
## WHERE EM SUBCONSULTAS:
```sql
SELECT p.name FROM products p WHERE stock >= 10 
AND (SELECT oi.product_id FROM order_items oi where oi.quantity >= 2);
``` 

Equivalente com JOIN -> provavelmente executará mais rapido.
```sql
SELECT p.name FROM products p INNER JOIN orders_items oi ON p.id = oi.products_id WHERE p.stock >= 10 AND oi.quantity >= 2;
``` 