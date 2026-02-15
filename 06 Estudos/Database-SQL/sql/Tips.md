***
**Criado em**: 2026-01-07  
**Modificado em**: 18:01
**Topico**: #sql
***
## Funcional > Otimizar

- A primeira etapa deve ser sempre focar em escrever um codigo funcional, independente se ele é lento
- A segunda etapa é focar na otimização melhorando o desempenho e legibilidade
***
O conteúdo de uma cláusula WHERE e de uma cláusula HAVING não pode ser intercambiado:
- Nunca insira uma condição com uma agregação na cláusula WHERE. Você verá uma mensagem de erro.
- Nunca insira uma condição na cláusula HAVING que não envolva uma agregação. Essas condições são avaliadas com muito mais eficiência na cláusula WHERE
***
-> Para substituir uma tabela existente
- Você pode usar `DROP TABLE` para excluir totalmente a tabela existente e depois criar uma nova tabela.
- Ou pode truncar a tabela existente, o que significa manter o esquema (também chamado de estrutura) da tabela, mas limpar os dados existentes nela. Isso pode ser feito com o uso de `DELETE FROM` para a exclusão dos dados da tabela
***