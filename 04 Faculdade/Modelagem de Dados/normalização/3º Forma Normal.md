***
**Criado em**: 2025-04-19  
**Modificado em**: 20:43
**Topico**: #normalização 
***
A 3º forma normal diz que atributos que não são chave devem ser independentes entre si e dependentes única e exclusivamente da chave primária da tabela. Não é permitido dependência transitiva. Adicionalmente, se a tabela está na 3ª. forma normal, automaticamente estará na 1ª. e na 2ª. formas normais também.

![3º forma normal](https://dhg1h5j42swfq.cloudfront.net/2022/09/01221427/3aformanormal.png)

Ex: No tabela acima é possivel a partir do campo "DATA_NASCIMENTO" calcular idade, entretanto, armazenar o campo idade nessa tabela seria incorreto.

Repare que ao adicionar o campo IDADE, tal campo não seria dependente da chave, mas sim de um atributo da tabela. Seria uma dependecia transitiva. Situação que fere a 3º forma normal.

DATA_NASCIMENTO depende da chave, mas IDADE não
IDADE depende indiretamente da CHAVE
[[Forma normal de Boyce-Codd]]
