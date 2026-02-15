***
**Criado em**: 2026-02-10  
**Modificado em**: 06:39
**Topico**: #
***
### Exclusão de uma tabela
```sql
DROP TABLE my_table;
```
***
### Exclusão de uma tabela com referências de chave externa

> Se outras tabelas tiverem chaves externas que referenciem a tabela que você está removendo, será preciso excluir as restrições de chave externa nas outras tabelas junto com a tabela que está sendo removida.

```postgresql
DROP TABLE my_table CASCADE;
```

> É perigoso usar CASCADE sem saber exatamente o que você está excluindo. Proceda com cuidado. Recomendo não executar esse comando a não ser que você tenha 100% de certeza de que não precisará das restrições.



