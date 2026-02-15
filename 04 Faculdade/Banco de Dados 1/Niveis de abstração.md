***
**Criado em**: 2026-02-12  
**Modificado em**: 07:01
**Topico**: #
***
A arquitetura ANSI/SPARC -> prevê multiplas visões de dados, um esquema conceitual (lógico) e um esquema interno (físico).

Um sistema de Banco de Dados se divide em tres niveis:
#### Nivel externo ->
Possui diversas descrições do BD de acordo com os grupos de usuarios.
#### Nivel conceitual ->
Descreve a estrutura de todo o BD para uma determinada comunidade de usuarios, ocultando detalhes sobre a organização física dos dados e apresentando a descrição logica dos dados e das ligações existentes entre eles.

#### Nível interno ->
Descreva a estrutura de armazenamento físico dos dados no BD, descreve o modelo físico dos dados que inclui detalhes sobre os caminhos de acesso aos dados internamente.
***
![[Pasted image 20260212071533.png]]

> Sobre os níveis de abstração de um banco de dados podemos pensar assim: Nível externo é o que o usuário pensa e quer e deseja visualizar, nível conceitual é como o projetista irá implementar o banco de dados, e nível interno é como estes dados serão armazenados, formas de acesso físico por exemplo


