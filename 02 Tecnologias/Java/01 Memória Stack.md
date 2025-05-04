***
**Criado em**: 2025-03-12  
**Modificado em**: 07:58
**Topico**: #java 
***
A memória **Stack** é responsavel por armazenar as chamadas de métodos do programa, seus argumentos, variaveis locais e referenciais a objetos. Sendo ela estática pré-alocada no start do programa e desalocada no final

A **Stack** também guarda informaçoes de Threads que estão em execução e variáveis primitivas locais.

> A alocação da memória stack normalmente é feita uma única alocação de um grande bloco e para cada argumento de função/método/procedure é destinada uma parte ou pedaço dessa memória. O Fato de a memória stack ter tamanho fixo especificado no projeto, faz dela potencial fonte de problemas se no caso for especificado tamanho menor do que se pretende usar no programa.

Apos a execução do metodo ele é retirado da **Stack**.

Em condições normais, **a _stack_ é alocada no início da execução da aplicação**, mais precisamente no início da _thread_, mesmo que a aplicação só tenha a _thread_ principal.
### Características

- É uma estrutura de dados LIFO (Last In, First Out).
- Cada thread tem sua própria pilha.
- O tamanho da pilha é limitado e fixo.
- A alocação e liberação de memória são rápidas, pois seguem uma ordem previsível.
- Quando um método é chamado, um novo bloco (frame) é criado na pilha para armazenar variáveis locais e informações do método. Quando o método termina, o bloco é removido.
- Se a pilha estourar (por exemplo, devido a recursão infinita), ocorre um `StackOverflowError`.
