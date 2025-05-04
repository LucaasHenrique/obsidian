[[FUNÇÕES DE STRING]]
## GROUP BY

O comando SQL para fazer essa operação de agregação é o group by.
Ele deverá ser utilizado logo após as cláusulas de condições where ou and,
e antes do order by, se a sua consulta possuí-lo. Vamos ao nosso código:


mysql> select c_codiclien, c_razaclien
from comclien, comvenda
where comvenda.n_numeclien = comclien.n_numeclien
group by c_codiclien, c_razaclien
order by c_razaclien;

## HAVING COUNT()

Agora, em nosso projeto, temos a necessidade de fazer um relatório que
traga como resultado os clientes que tiveram mais do que duas vendas. Para
isso, utilizaremos a função having count(), que será a condição para o
seu count(). Exemplificando, temos:

mysql> select c_razaclien, count(n_numevenda)
from comclien, comvenda
where comvenda.n_numeclien = comclien.n_numeclien
group by c_razaclien
having count(n_numevenda) > 2;

## AVG

Conseguimos extrair os valores das vendas, de sua quantidade, as maiores
e as menores etc. Porém, e se quisermos saber sua média, para comparar
períodos de datas? No MySQL temos o avg(), que busca a coluna cuja média
você deseja saber e realiza o cálculo. Vamos exemplificar consultando o valor
médio de todas as vendas:

mysql> select format(avg(n_totavenda),2)
from comvenda;

