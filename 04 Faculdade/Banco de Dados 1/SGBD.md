***
**Criado em**: 2026-02-12  
**Modificado em**: 07:20
**Topico**: #
***
Principais propriedades:

##### Controle de redundancia ->
A principal redundancia em DBs consiste no armazenamento de uma mesma informação em locais diferentes, o que pode provocar diversos problemas. 

Alguns destes problemas consistem inicialmente no aumento de esforço computacional para realizar a atualização destes dados; aumento do espaço necessário para o armazenamento dos dados. 

-> Em um sistema de BD **as informações só se encontram armazenadas em um único local** ou estão existindo duplicações controlada dos dados.
***
##### Compartilhamento de dados ->
um SGBD deve incluir um software para o controle de concorrência ao acesso dos dados em um ambiente multiusuário.

Ou seja deve  permitir o compartilhamento de dados, garantindo que se varios usuarios tentem realizar operações sobre um mesmo conjunto de dados, o resultado possa ser correto e consistente.
***
##### Controle de acesso ->
Um SGDB deve ter um subsistema de autorização e segurança para permitir que o DBA possa gerenciar as permissões que cada usuario tem sobre o banco de dados.
***
##### Multiplas interfaces ->
Usuarios com diferentes niveis tecnicos devem ter formas de interação com o DB condizente com o seu nivel. Um usuário tecnico pode utilizar de SQL, enquanto um usuário menos técnico pode saber usar apenas uma interface gráfica fornecida.
***
##### Representação de relacionamento complexo entre dados ->
Um SGBD deve ter a capacidade de representar uma variedade de relacionamentos complexos entre as tabelas.
***
##### Forçar restrições de integridade ->
Deve garantir a integridade nos dados do DB. Um exemplo de restrição é o tipo do dado, se é int, string ou bool, caso eu tente colocar uma string em um valor int o sgbd deve restringir a operação.
***
##### Garantir Backup e restauração de dados ->
um SGBD deve prover recursos para realização de cópias de segurança e restauração caso ocorra falhas de hardware ou software. O subsistema de backup e restauração do SGBD é o responsável pela restauração.
****
# Vantagens

##### Potencial para garantir padrões -> 
a abordagem de base de dados permite que o DBA defina e force a padronização entre os usuários da base de dados em grandes organizações. Isso facilita a comunicação e a cooperação entre vários  departamentos, projetos e usuários.
***
##### Redução do tempo de desenvolvimento de aplicações
Projetar e implementar uma nova base de dados pode tomar mais tempo do que escrever uma simples aplicação de arquivos especializada. Porém, uma vez que a base de dados esteja em uso, geralmente o tempo para se criar novas aplicações, usando-se os recursos de um SGBD, é bastante reduzido.
****
##### Independência de dados -> 
as aplicações de banco de dados não devem depender da forma como os dados estão representados e/ou armazenados.
****
##### Flexibilidade ->
pode ser necessario alterar a estrutura do banco de dados devido a mudanças nos requisitos. Um SGBD moderno permite que tais mudanças na estrutura da base de dados sejam realizadas sem afetar a maioria dos programas de aplicações existentes.
****
##### Disponibilidade para atualizar as informações ->
um SGBD disponibiliza o banco de dados para todos os usuários. Imediatamente após um usuário modificar uma base de dados, todos os outros usuários “sentem” imediatamente esta modificação.
****
#### Languages
#### DDL -> Data Definition Language

usada para criar, alterar, ou remover objetos do banco (tabelas, indices, etc...)

comandos -> [[CREATE]], ALTER, DROP, TRUNCATE, RENAME
***
#### DML -> Data Manipulation Language

usada para inserir, atualizar ou remover dados registrados

Comandos -> [[INSERT]], [[UPDATE]], DELETE
***
#### DQL -> Data Query Language

usada para fazer consulta no banco de dados

Comandos -> SELECT
***
#### DCL -> Data Control Language

utilizada para definir as permissões e segurança no db

Comandos -> GRANT, REVOKE
GRANT -> Concede permissões
REVOKE -> Remove permissões

```sql
GRANT SELECT ON usuarios TO lucas;
``` 
***
#### TCL -> Transaction Control Language

Controla as transações no banco. 

Comandos ->

`COMMIT` -> Confirma alterações
`ROLLBACK` -> Desfaz altereções
`SAVEPOINT` -> Cria ponto de salvamento
***
[[MER]]