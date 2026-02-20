***
**Criado em**: 2026-02-16  
**Modificado em**: 06:49
**Topico**: #
***
Representa os dados da base dados como uma coleção de relações. Podemos pensar que, cada relação pode ser entendida como uma tabela ou um simples arquivos de registros.

Cada linha de uma relação representa uma coleção de valores que estão relacionados. Esses valores podem ser interpretados como um fato que descreve uma entidade ou uma instância

-> Na linguagem do modelo relacional, cada linha é chamada de **tupla**, a coluna ou cabeçalho é chamado de **atributo** e a tabela de **relação**

**grau de uma relação** -> este é o número de atributos da relação.
***

**atributo-chave** -> usado para identificar de modo unívoco uma tupla em uma relação.

uma tabela pode ter mais de uma chave, nesse caso esse conjunto é chamado de chaves candidatas
***

**chave composta** -> utilização de mais de um atributo para formar a chave primária. exemplo: rg -> alem do numero, precisamos utilizar a UF como identificador.
***

**integridade referencial** -> responsavel por manter a consistência entre tuplas de duas relações.

uma tupla de uma tabela que se refere a outra tabela deve se referir a uma tupla existente naquela tabela.

exemplo: a tebela FUNCIONARIO tem o code_setor (FK) = 1, obrigatoriamente essa FK deve existir na tabela SETOR.
****
**Mapeamento**: MER -> MRel

**Passo 1: Mapeamento dos tipos de entidades** -> trasnformar entidades do MER em tabelas no MREL

**Passo 2: Mapeamento dos Conjuntos de Relacionamentos binários de razão de cardinalidade 1:1** -> 1. criar chave estrangeira em uma das relações;

**Passo 3: Mapeamento dos Conjuntos de Relacionamentos binários de razão de cardinalidade 1:N** -> Para o mapeamento 1:N a relação que mapeia o Conjunto de entidades do lado N recebe a chave primária do outro Conjunto de Entidades (lado 1) como chave estrangeira e os atributos do relacionamento.

**Passo 4: Mapeamento dos Conjuntos de Relacionamentos binários de razão de cardinalidade N:N** -> Criar uma nova tabela que representa o relacionamento, essa tabela carrega as chaves estrangeiras das duas tabelas envolvidas na relação.

**Passo 5: Mapeamento de Relacionamentos N-ários** -> Para os relacionamentos de grau maior que dois devemos criar uma nova relação (tabela) para representar o relacionamento. Temos que incluir também qualquer atributo simples do tipo de relacionamento n-ário.