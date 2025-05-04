### 1. **Usuário**

Cada usuário tem sua conta e deve ter acesso restrito aos seus próprios dados.

- Atributos: `id`, `nome`, `email`, `senha`, `dataCadastro`, `roles` (para controle de acesso).

### 2. **Categoria**

Ajuda a organizar as finanças, separando receitas e despesas em grupos.

- Atributos: `id`, `nome`, `tipo` (RECEITA ou DESPESA), `usuario`.

### 3. **Transação**

Registra uma movimentação financeira do usuário.

- Atributos: `id`, `descricao`, `valor`, `data`, `tipo` (RECEITA ou DESPESA), `categoria`, `usuario`.

### 4. **Meta Financeira**

Define objetivos de economia ou controle de gastos.

- Atributos: `id`, `descricao`, `valorMeta`, `dataLimite`, `usuario`.

### 5. **Conta Bancária**

Permite o controle de saldo e diferentes fontes de dinheiro.

- Atributos: `id`, `nome`, `saldo`, `usuario`.

### Relacionamentos principais:

- `Usuário` tem **muitas** `Transações`, `Metas Financeiras`, `Contas Bancárias` e `Categorias`.
- `Transação` pertence a um `Usuário` e tem **uma** `Categoria`.
- `Categoria` pertence a um `Usuário`, evitando que categorias de um usuário interfiram em outro.
- `Meta Financeira` pertence a um `Usuário`.
- `Conta Bancária` pertence a um `Usuário` e pode estar associada a uma `Transação`.