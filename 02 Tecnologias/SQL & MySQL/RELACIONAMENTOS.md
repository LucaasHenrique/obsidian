### 1. **OneToOne (Um para Um)**

- **Descrição**: Nesse tipo de relacionamento, uma instância de uma entidade está associada a exatamente uma instância de outra entidade, e vice-versa.

- **Exemplo**: Considere duas entidades, `Pessoa` e `CarteiraDeIdentidade`. Cada pessoa tem exatamente uma carteira de identidade, e cada carteira de identidade pertence a exatamente uma pessoa.

- **Uso comum**: Quando você tem uma relação direta e exclusiva entre duas entidades.

- A primary key de uma das tabelas é usada como **foreign key** (chave estrangeira) na outra tabela. 
---
### 2. **ManyToOne (Muitos para Um)**

- **Descrição**: Nesse tipo de relacionamento, várias instâncias de uma entidade podem estar associadas a uma única instância de outra entidade.

- **Exemplo**: Considere as entidades `Pedido` e `Cliente`. Muitos pedidos podem ser feitos por um único cliente, mas cada pedido está associado a apenas um cliente.

- **Uso comum**: Quando você tem uma relação onde muitos itens de uma entidade estão ligados a um único item de outra entidade.

- A tabela que representa o lado "muitos" carrega a **foreign key**, que referencia a primary key da tabela do lado "um".

---
### 3. **OneToMany (Um para Muitos)**

- **Descrição**: Este é o inverso do relacionamento `ManyToOne`. Uma instância de uma entidade pode estar associada a várias instâncias de outra entidade.

- **Exemplo**: Considere as entidades `Departamento` e `Funcionário`. Um departamento pode ter muitos funcionários, mas cada funcionário pertence a apenas um departamento.

- **Uso comum**: Quando você tem uma relação onde um item de uma entidade pode estar ligado a muitos itens de outra entidade.

- É semelhante ao ManyToOne. A tabela que representa o lado "muitos" carrega a **foreign key**, que referencia a primary key da tabela do lado "um".

---
### 4. **ManyToMany (Muitos para Muitos)**

- **Descrição**: Nesse tipo de relacionamento, várias instâncias de uma entidade podem estar associadas a várias instâncias de outra entidade.

- **Exemplo**: Considere as entidades `Aluno` e `Curso`. Um aluno pode se inscrever em muitos cursos, e um curso pode ter muitos alunos.

- **Uso comum**: Quando você tem uma relação onde muitos itens de uma entidade podem estar ligados a muitos itens de outra entidade. Em bancos de dados relacionais, isso geralmente é implementado usando uma tabela de junção (ou tabela associativa) que mapeia as relações entre as duas entidades.

-  Em relacionamentos ManyToMany, é necessário criar uma **tabela de junção** (ou tabela associativa) para mapear as relações entre as duas tabelas.
	- A tabela de junção contém **foreign keys** que referenciam as primary keys das duas tabelas envolvidas.
	- A primary key da tabela de junção pode ser uma **chave composta** (combinação das duas foreign keys) ou uma chave primária simples (um `id` adicional).