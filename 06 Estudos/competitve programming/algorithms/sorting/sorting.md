***
**Criado em**: 2025-07-29  
**Modificado em**: 21:13
**Topico**: #
***
-> Os algoritmos de ordenação eficientes funcionam em tempo O(n log n)

-> **inversao:** um par de elementos de array (array[a], array[b]) tal que a < b and array[a] > array[b], ou seja, os elementos estão na ordem errada.

-> número de inversões indica o quanto de trabalho é necessário para ordenar o array. Um array está completamente ordenado quando não há inversões

## Merge Sort
-> ordenação recursiva, metodo de divisão e conquista com complexidade de tempo O(n logn):

-> Se a = b, não faça nada, pois o subarray já está ordenado..
-> Calcule a posição do elemento do meio k = [(a + b)/2]
-> Ordene recursivamente o subarray array[a . . . k]
-> Ordene recursivamente o subarray array[k + 1 . . . b].
-> Junte os subarrays ordenados array[a . . . k] e array[k + 1 . . . b] em um subar-
ray ordenado array[a . . . b]

-> merge sort reduz pela metada o tamanho do subarray a cada passo. A recursão consiste em O( log n) níveis, e processar cada nível leva tempo O(n).
***

-> todo algoritimo com ordenação tem complexidade de O(nlogn)
