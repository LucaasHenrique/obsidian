***
**Criado em**: 2025-10-21  
**Modificado em**: 16:00
**Topico**: #
***
## Hierarquico
↪ modelo estruturado em forma de arvore genealogica. Utiliza a estrutura de dados do tipo arvore.

Nesse modelo (popular nos anos 60 e 70, como o IMS da IBM), os dados são organizados em níveis. Existe um registro "raiz" (o topo da árvore) e, abaixo dele, vêm os "filhos"

**Regra fundamental**: um registro "filho"  só pode ter um unico registro "pai".

para encontrar um determinado registro necessario seguir sequencialmente por cada registro pai

menos flexivel

ao tentar implementar multiplos relacionamentos geramos redundancias no armazenamento com dados duplicados 
***
## Modelo em Rede
↪ Conhecido como a evolução do modelo hierarquico. Retirou o conceito de hierarquia permitindo multiplos relacionamentos no BD.

Ele foi desenhado para resolver exatamente o problema que identificamos: relacionamentos "muitos-para-muitos" (N:M).

A grande mudança é: um registro "filho" (chamado de "membro") pode ter múltiplos "pais" (chamados de "donos").

Mudou a estrutura do tipo arvore para o tipo grafo permitindo multiplas conexoes.
****
## Modelo Relacional
↪ A ideal central era parar de usar "ponteiros" e "caminhos" fisicos

Em vez de usar estruturas complexas como arvores ou grafos, o modelo relacional armazena dados em tabelas simples (oficialmente chamadas de "relações").

cada **tabela** (relação) representa um tipo de "coisa" (alunos, cursos)
cada **linha** (tupla) da tabela representa um item especificoo (ex: Aluno C)
cada **coluna** (atributo) representa uma propriedade (ex: Nome do aluno)