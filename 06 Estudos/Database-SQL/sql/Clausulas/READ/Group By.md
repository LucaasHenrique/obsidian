***
**Criado em**: 2026-01-08  
**Modificado em**: 06:45
**Topico**: #sql
***
-> Sua finalidade é coletar linhas em grupos é resumi-las dentro dos grupos de alguma forma, acabando por retornar apenas uma linha por grupo.

```sql
SELECT t.name AS tour_name, COUNT(*) AS num_waterfalls FROM waterfall w INNER JOIN tour t ON w.id = t.stop GROUP BY t.name;
```

> Neste exemplo, COUNT(*) retorna o número de cachoeiras de cada passeio. No entanto, isso só ocorre porque cada linha de dados das tabelas waterfall e tour representa uma única cachoeira. Se uma cachoeira em particular estivesse listada em várias linhas, COUNT(*) forneceria um valor maior do que o esperado. Nesse caso, talvez você pudesse usar COUNT(DISTINCT waterfall_name) para encontrar as cachoeiras exclusivas. Mais detalhes podem ser encontrados em COUNT e DISTINCT. A principal lição a ser aprendida é que é importante confirmarmos manualmente os resultados da função de agregação para verificar se ela está resumindo os dados da maneira desejada.

```sql
SELECT u.name, COUNT(o.id) FROM users u INNER JOIN orders o on o.user_id = u.id GROUP BY u.id;
```

na consulta a acima `GROUP BY` agrupa cad pedido por usuario, cada usuario é considerado um grupo que possui um numero de pedido. Logo depois a agregação `COUNT(o.id)`  retorna o total de elementos do grupo.


com `GROUP BY u.id` estamos declarando que queremos examinar todas as linhas de dados e inserir os pedidos do Usuario de id = 1 em um grupo, todas os pedidos do usuario id = 2 em outro grupo e assim por diante.
***
## Na prática

Etapas para usar `GROUPY BY`:
1. Definir que coluna usar para separar, ou agrupar, os dados, no exemplo acima usei o id do usuario.
2. Definir como resumir os dados dentro de cada grupo, no exemplo realizo a contagem com `COUNT()`

Apos essas definições:
1. No select , listar as colunas pelas quais desejar fazer o agrupamento (id do usuario) e as agregações que deseja calcular dentro de cada grupo (Contagem de Pedidos);
2. Na clausula `GROUP BY` liste todas as colunas que não forem agregações (id do usuario);
***
read [[Order By]]
read [[Having]]
read [[Distinct]]
read [[Limit]]
***