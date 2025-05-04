alter table comclien drop column c_estclien

alter table comclien add column c_estclien varchar(50);

alter table comvenda add constraint fk_comprodu_comforne
foreign key(n_numeforne)
references comforne(n_numeforne)
on delete no action
on update no action;

update comclien set c_nomeclien = 'AARONSON FURNITURE'
where n_numeclien = 1;


create table pedidos (id_pedidos int primary key not null auto_increment, data DATE not null, id_cliente int, foreign key (id_cliente) references clientes(id_cliente));

## Criando tabelas por meio de select:

create table comclien_bkp as(
select *
from comclien
where c_estaclien = 'SP');

## Inserindo registros por meio de select:

insert into comcontato(
select n_numeclien,
c_nomeclien,
c_foneclien,
c_cidaclien,
c_estaclien,
n_numeclien
from comclien);

## Alterando registros por meio de select:

update comcontato set c_cidacontato = 'LONDRINA',
c_estacontato = 'PR'
where n_numeclien in ( select n_numeclien
from comclien_bkp);

## Deletando registros por meio de select:

delete from comcontato
where n_numeclien not in (select n_numeclien
from comvenda );

select c_codiprodu, c_descprodu
from comprodu
where substr(c_codiprodu,1,3) = '123'
and length(c_codiprodu) > 4;