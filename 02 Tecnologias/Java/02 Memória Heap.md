***
**Criado em**: 2025-03-12  
**Modificado em**: 07:58
**Topico**: #java
***
A memória **Heap** é utilizada para a alocação de objetos e desalocação no final do uso, ou seja, todos os objetos que vamos manipular no programa estarão armazenado na meḿoria Heap.

> O heap é considerado dinâmico. Em geral você aloca ou desaloca pequenos trechos de memória, só para a necessidade do dado. Esta alocação pode ocorrer fisicamente em qualquer parte livre da memória disponível para seu processo.

### Características

- É compartilhada por todas as threads da aplicação.
- O tamanho do heap pode crescer ou diminuir conforme necessário.
- A alocação de memória é mais lenta e menos previsível do que na pilha.
- Objetos no heap permanecem lá até que não haja mais referências a eles.
- Se o heap ficar sem memória, ocorre um `OutOfMemoryError`.