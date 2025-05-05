***
**Criado em**: 2025-05-05  
**Modificado em**: 10:05
**Topico**: #
***
# Resumo para Prova de Engenharia de Software

## 1. Conceitos Básicos de Engenharia de Software

- Engenharia de Software trata da criação, manutenção e evolução de software de forma sistemática, disciplinada e mensurável.
- Vai além da programação: inclui análise, projeto, testes, documentação, manutenção.
- Objetivos: garantir qualidade, reduzir custos e tempo, atender às necessidades do cliente.

### Características desejáveis:
- Confiável
- Eficiente
- Manutenível
- Evolutivo
- Utilizável

---

## 2. Processo de Desenvolvimento de Software (PDS)

- Conjunto de atividades organizadas para desenvolver um sistema.
- Define o fluxo, os papéis, os artefatos e as ferramentas usadas.

### Envolve:
- Planejamento
- Levantamento e especificação de requisitos
- Design (projeto de software)
- Implementação
- Testes
- Manutenção

---

## 3. Atividades comuns em todos os processos

1. **Especificação:** levantamento e documentação do que o sistema deve fazer.
2. **Projeto (Design):** definir a estrutura do sistema.
3. **Implementação:** codificação do sistema.
4. **Validação:** testes para garantir que o sistema atende aos requisitos.
5. **Evolução:** manutenção e melhorias.

---

## 4. Engenharia de Software Tradicional vs. Ágil

| Tradicional                   | Ágil                             |
| ----------------------------- | -------------------------------- |
| Planejamento pesado           | Planejamento leve e iterativo    |
| Etapas rígidas                | Iterações curtas                 |
| Pouca participação do cliente | Cliente envolvido frequentemente |
| Documentação extensa          | Documentação leve                |
| Mudanças são evitadas         | Mudanças são bem-vindas          |

### Motivação para o Ágil:
- Aumentar flexibilidade, velocidade de entrega, adaptação a mudanças, e proximidade com o cliente.

---

## 5. Etapas da Engenharia de Requisitos

1. **Análise e Negociação:** entender as necessidades e resolver conflitos.
2. **Especificação:** documentar requisitos de forma clara e objetiva.
3. **Validação:** garantir que os requisitos estão corretos e completos.
4. **Gerenciamento de Requisitos:** lidar com mudanças e controle de versões.

---

## 6. Requisitos Funcionais vs. Não Funcionais

### Funcionais:
- O que o sistema **deve fazer**.
- Ex: Permitir login, cadastro de usuário, envio de mensagens.

### Não Funcionais:
- **Qualidades** do sistema.
- Ex: desempenho, segurança, usabilidade, confiabilidade.

---

## 7. Modelagem sob o Paradigma Orientado a Objetos

- Foco em objetos que representam entidades do mundo real.
- Objetos contêm atributos (dados) e métodos (comportamentos).
- Melhora organização, manutenção e clareza do software.

---

## 8. Pilares da Orientação a Objetos

### Abstração
- Foco no essencial, ocultando detalhes desnecessários.
- Ex: classe `Carro` sem mostrar a complexidade do motor.

### Encapsulamento
- Proteção dos dados internos com acesso controlado.
- Ex: `private String senha;` com métodos `getSenha()` e `setSenha()`.

### Herança
- Reutilização de código entre classes.
- Ex: `Funcionario` herda de `Pessoa`.

### Polimorfismo
- Capacidade de um mesmo método agir de formas diferentes.
- Ex: `animal.emitirSom()` pode miar, latir ou rugir.

### Composição
- Objetos são formados por outros objetos.
- Ex: `Carro` possui `Motor`, `Roda`, `Painel`.

---