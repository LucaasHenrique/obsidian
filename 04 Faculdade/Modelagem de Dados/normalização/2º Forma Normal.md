***
**Criado em**: 2025-04-19  
**Modificado em**: 15:49
**Topico**: #normalização 
***
Na 2º forma normal todos os atributos que não são chave devem depender unicamente da chave primária da tabela. Em outras palavras, não pode haver dependência parcial. 

![2º Forma Normal](https://dhg1h5j42swfq.cloudfront.net/2022/09/01221337/2aformanormalremuneracao.png)

alt: A tabela representa a remuneração de um professor em determinado período.

As remunerações são variáveis de acordo com o número de aulas ministradas no mês. Por este motivo, o valor depende do período e do professor. Nesse caso, podemos dizer que a tabela está na 2ª. forma normal.

Se o valor dependesse apenas do professor, por exemplo, sem considerar o período, estaríamos diante de uma dependência parcial. Neste caso, o exemplo não estaria na 2ª. forma normal, mas estaria na 1ª.

basicamente se o valor dependesse de somento um dois campos seria um caso de dependencia parcial.

[[3º Forma Normal]]