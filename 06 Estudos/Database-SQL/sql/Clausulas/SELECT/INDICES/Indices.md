	***
**Criado em**: 2026-02-10  
**Modificado em**: 06:52
**Topico**: #
***
Um consulta numa tabela de 10 milhões de linhas buscando todos os dados que foram inseridos na data 01-01-2021 levaria muito tempo para ser executada, pois seria necessario andar toda a tabela verificando a correspondencia com a data.

-> Em termos de algoritmos isso seria equivalente uma busca liner O(n);

No sql um indice é um atalho para se encontrar informações de forma rapida. 

Pense que estamos lendo o livro "sociedade do cansaço" e queremos ir para o capitulo "tedio profundo", sem um índice (sumario) deveriamos olhar pagina por pagina ate encontrar a correta, mas com um índice poderiamos simplesmente ir para a pagina correta.

-> Porem índices ocupam muito espaço, devemos ter cuidado em sua criação

Criamos o índice parra os email de usuarios;
```sql
CREATE INDEX idx_email ON users(email);
``` 

agora a consulta pode ser mais rapida:
```sql
SELECT * FROM users WHERE email = 'ana@email.com'; 
```
***
também podemos criar índices compostos
```sql 
CREATE INDEX my_index ON my_table (log_date, team);
``` 

o detalhe é que a ordem importa na filtragem pelas colunas:

> • Pelas duas colunas: o índice acelerará a consulta. 
> • Pela primeira coluna (log_date): o índice acelerará a consulta. 
> • Pela segunda coluna: (team): o índice não ajudará porque primeiro ele organizará os dados por log_date e depois pela coluna team.

***
Para excluir um índice basta fazer um:
```Postgresql
DROP INDEX my_index;
``` 
***
