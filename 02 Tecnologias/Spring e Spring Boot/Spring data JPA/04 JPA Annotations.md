***
**Criado em**: 2025-03-08  
**Modificado em**: 20:27
**Topico**: #JPA
***
## @OneToMany

## @ManyToOne

## @OneToMany

## @ManyToMany


**FetchType.LAZY** ➡ No momento de busca da entindades, as entidades relacionadas só serão consultadas quando necessário.

**FetchType.EAGER** ➡ No momento de busca da entindades, todas as entidades relacionadas serão consultadas.

**CascadeType.ALL** ➡ Sempre q acontecer uma transação de um dos lados da relação, será replicada para o outro lado.
↪
- ex: a relação OneToOne entre a entidade livro e a review, caso um livro seja deletado, a review vinculada a esse livro tbm será.