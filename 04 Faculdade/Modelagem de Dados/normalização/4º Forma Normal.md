***
**Criado em**: 2025-04-19  
**Modificado em**: 21:27
**Topico**: #normalização 
***
Uma tabela está na 4º forma normal se não possuir dependencias multivaloradas.

Se existem atributos que podem conter multiplos valores iguais na mesma tabela, é necessário isalá-los e promover suas decomposições em subconjuntos.

EX: cidade e ano de ingresso

| ID_CIDADE(PK) | CIDADE         |
| ------------- | -------------- |
| 1             | Belém          |
| 2             | Rio de Janeiro |
| 3             | Campinas       |

| ID_ANO(PK) | ANO_INGRESSO |
| ---------- | ------------ |
| 1          | 2023         |
| 2          | 2024         |
| 3          | 2025         |

| ID_PROF(PK) | NOME           | ID_CIDADE(FK) | ID_ANO(FK) |
| ----------- | -------------- | ------------- | ---------- |
| 1           | LUCAS HENRIQUE | 1             | 2          |
| 2           | ANDRE CASTRO   | 3             | 3          |
***