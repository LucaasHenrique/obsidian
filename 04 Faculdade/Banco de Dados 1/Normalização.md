***
**Criado em**: 2026-02-19  
**Modificado em**: 06:38
**Topico**: #
***
Normalização é o processo de organizar as tabelas e colunas de um banco de dados relacional para reduzir redundância de dados e melhorar a integridade das informações. O objetivo principal é garantir que cada dado seja armazenado em apenas um lugar.

Sem normalização temos:
- **Redundância** -> repetição de dados em vários lugares
- **Anomalias de inserção** -> dificuldade de adicionar dados sem inserir informações incompletas.
- **Anomalias de atualização** -> mudar um dado exige atualizar várias linhas 
- **Anomalias de exclusão** -> apagar um registro pode apagar dados importantes indevidamente.
****
**1° Forma Normal** -> diz que todos os atributos devem conter um valor atômico (único), não deve haver repetições nem atributos multivalorados.

ex: Tabela Nota Fisca -> id = 1 | produto ={Notebook, Celular, Teclado}

- Elimina grupos repetitidos;

Para eliminar essa anomalia é necessário dividir a tabela em duas, criando uma tabela só para itens da nota e uma só para nota é fazer o relacionamentos entre elas. Nesse caso 1:N;

**Nota** (número da nota, data, cliente, RG, CPF, endereço, nº, bairro, cidade, UF, valor_total).

**itens_nota** -> (**número_da_nota, código_produto**, quantidade, valor_unitário, valor_total);
 
 **Produto** -> (**código**, descrição, unidade_de_medida, valor_unitário);

***
**2° Forma Normal** -> Elimina dependência parciais. Todos os atributos não chave devem depender da chave completamente.

Tabela Nota Fiscal

id_nota | id_cliente | CPF | RG | endereço | nº | bairro | cidade | UF | valor_total

veja que id_cliente depende de id_nota, porem CPF e RG dependem do id_cliente sem qualquer relação com id_nota, logo, temos uma dependência parcial.

cidade e UF também não possuem relação com id_nota.

para resolver esses problemas criamos tabelas para esses atributos com dependência parcial.

**Cliente** -> (**código**, nome, RG, CPF);
**Cidade** -> (**código**, descrição, UF);
***

**3° Forma Normal** -> diz que todo atributo precisa estar na segunda forma normal e não deve haver dependencia transitiva entre atributos, isto é, quando um atributo não depende de outro atributo não chave que depende da chave primaria. Ou seja, esse atributo depedende transtivamente da pk;

ex: cliente_cidade depende de cliente que depende de pedido_id;
cliente_cidade -> cliente -> pedido_id;

A solução é criar uma nova tabela utilizando cliente como pk;

Clientes:

| cliente | cliente_cidade |
| ana      | campinas         |
| joao     | rio de janeiro   |

Pedidos: 

| pedido_id | cliente     |
| 1                | ana          |
***
more exemples: https://aprendamais.mec.gov.br/mod/page/view.php?id=116429


