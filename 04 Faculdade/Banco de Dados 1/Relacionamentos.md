***
**Criado em**: 2026-02-14  
**Modificado em**: 19:28
**Topico**: #
***
-> Nenhuma informação armezanada em um banco de dados existe de forma isolada
-> Normalmente relacionamentos representam ações fisicas ou formas de dependência entre os elementos envolvidos.
-> Um relacionamento é uma associação entre diversas entidades.
***
Considere o relacionamento `TRABALHA` e as entidades `EMPREGADO` e `DEPARTAMENTO`.

o relacionamento associa cada `EMPREGADO` a um `DEPARTAMENTO`

exemplo: o `EMPREGADO`João `TRABALHA` no `DEPARTAMENTO` de computação
***
### Grau de relacionamento
-> O grau de um conjunto de relacionamentos indica o número de conjuntos de entidades participantes

-> Um tipo de relacionamento de grau dois é chamado binário, de grau três de ternário, de grau quatro quaternário, acima disso, n-ário. 
***
`Unário` -> Grau de relacionamento que envolve apenas um tipo de entidade;

exemplo: casamento é um relacionamento entre duas pessoas;
***
`Binário` -> envolve dois tipos de entidade

exemplo:   `FUNCIONÁRIO` -> `PRODUZ` -> `PRODUTO`, `PRODUZ` é o relacionamento
***
`Ternário`-> envolve três tipos de entidadaes

exemplo: [[ternario.canvas]]
***
`Quarternário` -> envolve quatro tipos de relacionamentos

exemplo: [[quarternario.canvas]]
***
- A **Cardinalidade Mínima** determina a quantidade mínima de Entidades relacionadas por um número representativo, ou seja, 0 (zero) 1, 2, ...., N (muitos);
- A **Cardinalidade Máxima** determina a quantidade máxima de Entidades relacionadas por um número representativo, ou seja, 1, 2, ...., N (muitos).
***
