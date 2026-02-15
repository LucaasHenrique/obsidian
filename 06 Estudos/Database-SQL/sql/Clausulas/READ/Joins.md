***
**Criado em**: 2026-01-07  
**Modificado em**: 07:15
**Topico**: #sql
***
## JOIN usa como padrão INNER JOIN
- A boa pratica é usar INNER JOIN

Uma cláusula JOIN é sempre seguida de uma cláusula ON, que especifica como as tabelas devem ser vinculadas:

```sql
SELECT * FROM waterfall w JOIN tour t ON w.id = t.stop;
```

Neste caso, o id da cachoeira na tabela waterfall deve coincidir com a parada (stop) na cachoeira da tabela tour
***
read [[Group By]]
