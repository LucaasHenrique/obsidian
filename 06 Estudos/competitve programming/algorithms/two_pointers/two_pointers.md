***
**Criado em**: 2025-09-20  
**Modificado em**: 17:07
**Topico**: #
***
O que é Two Pointers

O Two Pointers é uma técnica usada para percorrer estruturas como arrays ou listas com dois índices (ponteiros), geralmente para otimizar a busca, soma, subarrays ou comparações, reduzindo complexidade de tempo de  O(n²) para O(n) ou O(nlog⁡n).

Ideia principal:

- Você tem dois ponteiros que percorrem o array:
	 - i começa no início
	-  j começa no final

Dependendo da condição, você move um ou outro ponteiro até encontrar a solução

```c++
#include <bits/stdc++.h>
using namespace std;

int main() {
    vector<int> arr = {1, 2, 4, 6, 8, 11};
    int target = 10;

    int i = 0;             // ponteiro inicial
    int j = arr.size() - 1; // ponteiro final

    while (i < j) {
        int sum = arr[i] + arr[j];
        if (sum == target) {
            cout << "Par encontrado: " << arr[i] << ", " << arr[j] << "\n";
            break;
        } else if (sum < target) {
            i++;  // aumentar a soma
        } else {
            j--;  // diminuir a soma
        }
    }
}

```