***
**Criado em**: 2025-04-19  
**Modificado em**: 21:01
**Topico**: #normalização 
***
Nesta forma normal, todo atributo não chave precisa depender funcionalmente diretamente da chave, seja ela primária ou candidata. Em outras palavras, não pode haver dependências entre os atributos não chave.

>**Todo determinante (atributo que define outro) deve ser uma chave candidata.**

- Todos os atributos não-chave devem depender exclusivamente da chave primária ou de uma chave candidata.
- Não pode existir nenhuma dependência funcional onde um atributo não-chave determine outro atributo.
***
Suponha uma tabela **`Matrícula`** que registra alunos, disciplinas e professores:

| **Aluno** | **Disciplina** | **Professor** |
| --------- | -------------- | ------------- |
| João      | Matemática     | Carlos        |
| Maria     | Física         | Ana           |
| Pedro     | Matemática     | Carlos        |

#### **Problema (viola a BCNF, mas está na 3FN):**

- **Chave candidata (PK):** `(Aluno, Disciplina)` (um aluno pode se matricular em várias disciplinas).
    
- **Dependência funcional:** `Disciplina → Professor` (cada disciplina tem apenas um professor).
    
    - Aqui, `Disciplina` **não é uma chave candidata**, mas determina `Professor`. Isso **viola a BCNF**, pois um **não-chave (`Disciplina`)** está determinando outro atributo.

***
Dividir em duas tabelas:

1. **`Matrícula_Aluno`** (relaciona aluno e disciplina):
    
    |**Aluno**|**Disciplina**|
    |João|Matemática|
    |Maria|Física|
    |Pedro|Matemática|
    
2. **`Disciplina_Professor`** (relaciona disciplina e professor):

    |**Disciplina (PK)**|**Professor**|
    |---|---|
    |Matemática|Carlos|
    |Física|Ana|
    

Agora:

- **`Disciplina`** é uma **chave primária** na segunda tabela, então `Disciplina → Professor` **não viola a BCNF**.
    
- Eliminamos redundâncias e anomalias.
    
---
[[4º Forma Normal]]