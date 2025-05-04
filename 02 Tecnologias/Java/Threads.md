***
**Criado em**: 2025-03-19  
**Modificado em**: 21:25
**Topico**: #java 
***
## No sistema operacional

É uma forma de um processo se dividir em uma ou mais tarefas.

>Pense numa _thread_ como uma sequência de comandos sendo executados em um programa. Se você tiver duas _threads_, terá duas sequências de comandos executando ao mesmo tempo **no mesmo programa** ou processo.

Executar uma programa duas vezes não cria duas threads é sim criar dois processos. Threads existem e rodam concorrentemente num mesmo processo. Processos executam concorrentemente em um mesmo sistema operacional.

>As threads de um processo compartilham o chamado contexto de execução, o que, em termos simples, significa que todas têm a mesma visão da memória ocupada pelo processo. Com isso, as variáveis e funções de uma thread também podem ser acessadas por outras threads.

Processos não compartilham memória, então existe uma dificuldade na comunicação entre dois processos. Com threads esse processo se torna mais simples.

>O uso de _threads_ começa a ficar interessante quando você quer executar pelo menos duas coisas ao mesmo tempo em um programa para tirar vantagem da múltiplas CPUs ou ainda para evitar que o programa inteiro fique travado ao executar uma operação demorada.

## No java

No java uma **Thread** é um objeto da class **java.lang.thread** que permite a execução de sequencias de instruções em uma Thread da maquina virtual, que nesse caso é executada por uma Thread do sistema operacional hospodeiro.

sistema operacional hospedeiro ➡ sistema onde a maquina virtual está sendo executada.

>Essas sequências de instruções são encapsuladas dentro de um método `run()` que é passado para o construtor da `Thread` (não o método diretamente, mas um objeto `Runnable`, isto é, que implementa a interface `Runnable` e que portanto implementa o método `run()`). Ou, alternativamente, uma vez que a própria classe `Thread` já implementa `Runnable`, você pode optar por simplesmente implementar esse método no próprio objeto da classe `Thread`.  

Porém, somente dar um método `run()` à `Thread` não a faz rodar em paralelo a outras _threads_. É necessário iniciá-la chamando o método `Thread.start()`.

