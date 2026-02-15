***
**Criado em**: 2026-01-07  
**Modificado em**: 16:37
**Topico**: #sql
***
Todas as consultas SQL conterão alguma combinação dessas cláusulas. Você pode não se lembrar do restante, mas precisa se lembrar dessa ordem! 
SELECT -- colunas a serem exibidas 
FROM -- tabelas de onde será executada a extração 
WHERE -- filtra linhas 
GROUP BY -- divide linhas em grupos 
HAVING -- filtra linhas agrupadas 
ORDER BY -- colunas a serem classificadas
***
## Ordem de Execução de SQL:

1. FROM 
2. WHERE 
3. GROUP BY 
4. HAVING 
5. SELECT 
6. ORDER BY
***
1. Coleta todos os dados com FROM 
2. Filtra linhas de dados com WHERE 
3. Agrupa as linhas com GROUP BY 
4. Filtra linhas agrupadas com HAVING 
5. Especifica as colunas a serem exibidas com SELECT 
6. Reorganiza os resultados com ORDER BY