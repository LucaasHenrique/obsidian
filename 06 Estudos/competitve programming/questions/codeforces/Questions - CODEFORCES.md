***
**Criado em**: 2026-02-03  
**Modificado em**: 21:31
**Topico**: #
***
1 -> SwapSort
Answer -> A resposta consiste apenas em guardar o menor elemento que apareceu ate agr é trocalo de posição.

Para isso basta é necessario realizar um brute force no vetor, comparar a posição com todo o restante do vetor e pegar o minimo. 
```cpp
for (int i = 0; i < n; i++) {
        int m = i;
        for (int t = i;  t < n; t++) {
           if (a[m] > a[t]) {
               m = t;
           } 
        }
        if (i != m)
            p.pb({i, m});
        swap(a[i], a[m]);
    }
``` 
***
Complexidade O(n²);