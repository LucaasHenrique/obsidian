# Threads em Computação: Baixo Nível, Alto Nível, Paralelismo e Concorrência

## Índice
- [O que são Threads?](#o-que-são-threads)
- [Threads em Baixo Nível](#threads-em-baixo-nível)
- [Threads em Alto Nível](#threads-em-alto-nível)
- [Comportamento Assíncrono vs Paralelo](#comportamento-assíncrono-vs-paralelo)
- [Paralelismo vs Concorrência: Entendimento Profundo](#paralelismo-vs-concorrência-entendimento-profundo)
- [Problemas Específicos](#problemas-específicos-de-cada-abordagem)
- [Quando Usar Cada Abordagem](#quando-usar-cada-abordagem)

---

## O que são Threads?

**Threads** (ou "linhas de execução") são a menor unidade de processamento que pode ser agendada por um sistema operacional. Imagine um programa como uma fábrica: uma thread seria uma linha de produção dentro dessa fábrica.

---

## Threads em Baixo Nível

Em **baixo nível**, estamos falando da implementação diretamente no sistema operacional e hardware:

### Threads do Kernel (Kernel Threads)

O sistema operacional gerencia diretamente essas threads. Cada uma tem seu próprio contexto de execução (registradores da CPU, pilha, contador de programa). O SO faz o **escalonamento** (scheduling), decidindo qual thread executará em qual núcleo do processador e por quanto tempo.

### Como Funcionam

Quando o SO cria uma thread, ele aloca recursos como pilha de memória e estruturas de controle. O processador alterna entre threads através de **context switching** - salvando o estado de uma thread e carregando o estado de outra. Isso acontece milhares de vezes por segundo.

### Custo

Criar e gerenciar threads do kernel é relativamente "pesado" porque envolve chamadas ao sistema operacional (syscalls), que são operações custosas.

---

## Threads em Alto Nível

Em **alto nível**, temos abstrações fornecidas pelas linguagens de programação:

### Green Threads ou User-Space Threads

São threads gerenciadas pela própria linguagem/runtime, não pelo SO. A linguagem decide como multiplexar várias threads leves sobre poucas threads do kernel.

### Thread Pools

Conjuntos de threads reutilizáveis que executam tarefas sob demanda, evitando o custo de criar/destruir threads constantemente.

### Async/Await

Abstrações modernas que permitem programação concorrente sem necessariamente criar múltiplas threads.

---

## Comportamento Assíncrono vs Paralelo

### Paralelismo

**O que é**: Execução **simultânea** de múltiplas tarefas em múltiplos núcleos de CPU ao mesmo tempo.

**Exemplo**: Você tem 4 núcleos de CPU processando 4 threads diferentes simultaneamente - 4 cálculos matemáticos complexos acontecendo literalmente ao mesmo tempo.

**Para que serve**: Acelerar tarefas que exigem muito processamento (CPU-bound), como renderização de vídeo, cálculos científicos, processamento de imagens.

### Assincronismo

**O que é**: Execução **concorrente** onde tarefas progridem sem necessariamente executar ao mesmo tempo. Uma thread pode iniciar uma operação e, enquanto espera (I/O, rede, disco), fazer outra coisa.

**Exemplo**: Um servidor web com uma thread pode atender milhares de requisições. Enquanto espera a resposta do banco de dados para o usuário A, processa a requisição do usuário B, e enquanto espera o disco ler um arquivo para C, envia resposta para D.

**Para que serve**: Otimizar tarefas que passam muito tempo esperando (I/O-bound), como servidores web, aplicações de rede, leitura/escrita de arquivos.

### Como Funcionam na Prática

**Paralelo com threads**:
```
Thread 1 (Núcleo 1): [====PROCESSANDO====]
Thread 2 (Núcleo 2): [====PROCESSANDO====]
Thread 3 (Núcleo 3): [====PROCESSANDO====]
```

**Assíncrono (pode ser 1 thread)**:
```
Thread única:
[Inicia requisição A] → [Inicia requisição B] → 
[Processa resposta A] → [Inicia requisição C] → 
[Processa resposta B] → [Processa resposta C]
```

### Casos de Uso

**Use threads paralelas quando**: Você precisa fazer cálculos pesados e tem múltiplos núcleos disponíveis (processamento de imagem, machine learning, simulações).

**Use programação assíncrona quando**: Você tem muitas operações de I/O (servidores web, scraping, APIs que fazem múltiplas chamadas externas).

**Combine ambos**: Servidores modernos frequentemente usam um pool de threads (paralelismo) onde cada thread executa código assíncrono (para lidar com múltiplas conexões simultaneamente).

---

## Paralelismo vs Concorrência: Entendimento Profundo

### A Diferença Fundamental

**Concorrência** é sobre **estrutura** - como você organiza seu programa para lidar com múltiplas tarefas.

**Paralelismo** é sobre **execução** - múltiplas tarefas realmente acontecendo ao mesmo tempo.

> Uma frase famosa do criador da linguagem Go, Rob Pike: 
> *"Concorrência é sobre lidar com muitas coisas ao mesmo tempo. Paralelismo é sobre fazer muitas coisas ao mesmo tempo."*

---

## Concorrência Detalhada

### O que realmente significa

Concorrência significa que seu programa está **estruturado** para progredir em múltiplas tarefas, mesmo que apenas uma execute por vez. É sobre gerenciar múltiplos fluxos de execução que podem se intercalar.

### Como funciona com threads

**Cenário: 1 núcleo de CPU, 3 threads**

```
Tempo →
Thread 1: [████]----[███]------[████]---
Thread 2: ----[███]------[████]----[██]
Thread 3: --------[██]----------[███]---
         (apenas 1 executa por vez)
```

O sistema operacional faz **time-slicing** (fatias de tempo): cada thread executa por alguns milissegundos, depois o SO faz um **context switch** para outra thread. Isso acontece tão rápido que parece que todas estão executando "ao mesmo tempo", mas não estão.

### Context Switching - O Mecanismo

Quando o SO troca de uma thread para outra:

1. **Salva o contexto** da thread atual (registradores da CPU, contador de programa, ponteiro da pilha)
2. **Escolhe** qual thread executar a seguir (algoritmos: round-robin, prioridade, etc)
3. **Carrega o contexto** da próxima thread
4. **Retoma** a execução da nova thread

Isso tem **custo**: salvar/restaurar estado, invalidar cache da CPU, etc. Por isso context switches frequentes podem degradar performance.

### Exemplo Prático de Concorrência

```
Thread servidor web (1 núcleo):
1. Recebe requisição do Cliente A → processa → aguarda banco de dados
   ↓ (context switch - thread bloqueia esperando I/O)
2. Recebe requisição do Cliente B → processa → aguarda disco
   ↓ (context switch)
3. Banco responde para A → finaliza resposta A
   ↓ (context switch)
4. Disco responde para B → finaliza resposta B
```

Aqui, **uma única thread** está lidando com 2 clientes de forma **concorrente**. Enquanto espera I/O de um, processa outro.

---

## Paralelismo Detalhado

### O que realmente significa

Paralelismo significa que múltiplas threads estão **literalmente executando ao mesmo tempo** em diferentes núcleos da CPU. Requer hardware com múltiplos núcleos/processadores.

### Como funciona com threads

**Cenário: 4 núcleos de CPU, 4 threads**

```
Tempo →
Núcleo 1 - Thread 1: [████████████████]
Núcleo 2 - Thread 2: [████████████████]
Núcleo 3 - Thread 3: [████████████████]
Núcleo 4 - Thread 4: [████████████████]
         (todas executam simultaneamente)
```

Cada núcleo físico executa uma thread diferente **ao mesmo tempo**. Não há intercalação - é execução verdadeiramente simultânea.

### Exemplo Prático de Paralelismo

```
Processar imagem de 4000x3000 pixels:
Thread 1 (Núcleo 1): processa linhas 0-999      [executando]
Thread 2 (Núcleo 2): processa linhas 1000-1999  [executando]
Thread 3 (Núcleo 3): processa linhas 2000-2999  [executando]
Thread 4 (Núcleo 4): processa linhas 3000-3999  [executando]

Todas literalmente processando pixels AO MESMO TEMPO.
```

---

## A Relação Entre Concorrência e Paralelismo

### Podem existir independentemente

- **Concorrência SEM paralelismo**: Múltiplas threads em 1 núcleo (intercaladas)
- **Paralelismo SEM concorrência**: 1 programa sequencial que usa instruções SIMD (Single Instruction Multiple Data) do processador
- **Concorrência COM paralelismo**: Múltiplas threads em múltiplos núcleos (o cenário mais comum hoje)

### Cenário Real: 8 threads, 4 núcleos

```
Núcleo 1: [Thread1][Thread5][Thread1][Thread5]...
Núcleo 2: [Thread2][Thread6][Thread2][Thread6]...
Núcleo 3: [Thread3][Thread7][Thread3][Thread7]...
Núcleo 4: [Thread4][Thread8][Thread4][Thread8]...
```

Aqui temos:
- **Paralelismo**: 4 threads executando simultaneamente (uma por núcleo)
- **Concorrência**: 8 threads competindo por 4 núcleos (com context switching)

---

## Problemas Específicos de Cada Abordagem

### Problemas de Concorrência

#### Race Conditions

Quando múltiplas threads acessam dados compartilhados e o resultado depende da ordem de execução.

```
Conta bancária: saldo = 100

Thread 1: ler saldo (100) → adicionar 50 → escrever (150)
Thread 2: ler saldo (100) → subtrair 30 → escrever (70)

Se intercalarem mal:
T1 lê: 100
T2 lê: 100 (ainda não viu a escrita de T1!)
T1 escreve: 150
T2 escreve: 70 (sobrescreve!)

Resultado: 70 (perdemos os +50!)
```

#### Deadlocks

Threads esperando umas pelas outras eternamente.

```
Thread 1: trava recurso A → espera recurso B
Thread 2: trava recurso B → espera recurso A
(ambas ficam travadas para sempre)
```

### Problemas de Paralelismo

#### False Sharing

Quando threads em núcleos diferentes modificam variáveis que estão na mesma linha de cache da CPU.

```
CPU1                    CPU2
cache: [var1][var2] ← cache: [var1][var2]
Thread1 modifica var1   Thread2 modifica var2

Mesmo sendo variáveis diferentes, estão na mesma linha de cache!
Resultado: invalidação constante de cache, degradando performance.
```

#### Contenção de Recursos

Quando múltiplas threads paralelas competem pelo mesmo recurso (memória, lock).

---

## Quando Usar Cada Abordagem

### Use Concorrência (pode ser 1 núcleo)

- **Servidores web/API**: Lidar com milhares de conexões simultâneas
- **GUIs**: Manter interface responsiva enquanto faz operações em background
- **I/O pesado**: Download de arquivos, consultas a banco de dados
- **Tarefas que passam muito tempo esperando**

**Benefício**: Melhor utilização de recursos, responsividade

### Use Paralelismo (requer múltiplos núcleos)

- **Processamento de imagens/vídeo**: Aplicar filtros, renderização
- **Cálculos científicos**: Simulações, análise de dados massivos
- **Machine Learning**: Treinamento de modelos
- **Tarefas CPU-bound** (limitadas pela velocidade do processador)

**Benefício**: Speedup real - termina mais rápido

### Combine Ambos

**Exemplo: Servidor de processamento de imagens**

```
Thread Pool (paralelismo): 8 threads workers
Cada thread (concorrência): 
  - Recebe requisição (async)
  - Baixa imagem (async I/O)
  - Processa imagem (paralelo com outras threads)
  - Upload resultado (async I/O)
  - Próxima requisição
```

---

## Medindo o Ganho

### Lei de Amdahl

Nem tudo pode ser paralelizado.

Se 50% do seu programa pode rodar em paralelo com 4 núcleos:
- Speedup máximo teórico: ~1.6x (não 4x!)
- Porque os outros 50% ainda rodam sequencialmente

### Sobrecarga

Criar threads, sincronização, context switches tem custo. Às vezes, usar muitas threads deixa o programa mais lento que usar poucas.

---

## Resumo Visual

```
CONCORRÊNCIA (estrutura/organização):
1 garçom atendendo 5 mesas
→ vai de mesa em mesa
→ todas progridem, mas ele só está em 1 por vez

PARALELISMO (execução simultânea):
5 garçons atendendo 5 mesas
→ cada um em sua mesa
→ todas progridem simultaneamente

CONCORRÊNCIA + PARALELISMO:
3 garçons atendendo 10 mesas
→ cada garçom alterna entre ~3 mesas (concorrência)
→ mas os 3 trabalham ao mesmo tempo (paralelismo)
```

---

## Conclusão

A chave é entender: **concorrência** é sobre como você **estrutura** o problema (gerenciamento de múltiplas tarefas), enquanto **paralelismo** é sobre como **executa** (aproveitando múltiplos núcleos para velocidade bruta).

A escolha entre essas abordagens depende do tipo de problema que você está resolvendo e das características da sua aplicação.
