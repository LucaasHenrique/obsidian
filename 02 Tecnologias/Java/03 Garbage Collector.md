***
**Criado em**: 2025-03-12  
**Modificado em**: 10:21
**Topico**: #java
***
O **Garbage Collector** é responsavel por realizar de forma automatica o gerenciamento de memória. Ele atua na [[02 Memória Heap]], sendo responsável por liberar a memória alocada para objetos que não estão mais em uso pelo programa, deixando a memória que ele ocupavam disponível novamente evitando vazamentos de memória e simplificando o desenvolvimento, já que os programadores não precisam gerenciar manualmente a alocação e liberação de memória
***
### Funcionamento

1. **Alocação de Memória**: Quando um objeto é criado em Java, ele é alocado na memória heap.
2. **Identificação de Objetos Inúteis**: O GC identifica os objetos que não estão mais sendo referenciados pelo programa (ou seja, objetos que não podem mais ser acessados).
3. **Coleta de Lixo**: O GC libera a memória ocupada por esses objetos, permitindo que ela seja reutilizada para novas alocações.

Caso exista somente uma Thread de execução pode ser necessário a interrupção momentanea do programa em execução para que o garbage collector realize a limpeza. Essa interrupção é conhecida como **"stop-the-world"** (parar o mundo). Esse é o caso do Serial GC, um garbage collector que possui somente uma thread.
***
### Tipos

1. **Serial GC**: Usa um único thread para realizar a coleta de lixo. É adequado para aplicações simples ou ambientes com recursos limitados.
2. **Parallel GC (Throughput Collector)**: Usa múltiplos threads para realizar a coleta de lixo, melhorando o desempenho em aplicações que exigem alta taxa de processamento.
3. **G1 GC (Garbage-First Collector)**: Projetado para aplicações que precisam de baixa latência e grandes heaps de memória. Divide a heap em regiões e prioriza a coleta nas regiões com mais "lixo".
4. **ZGC (Z Garbage Collector)**: Introduzido no Java 11, é um coletor de lixo de baixa latência que pode lidar com heaps de memória muito grandes (terabytes) com pausas mínimas.
5. **Shenandoah GC**: Também focado em baixa latência, reduzindo o tempo de pausa durante a coleta de lixo.
***