***
**Criado em**: 2025-10-25  
**Modificado em**: 15:52
**Topico**: #
***
						A ideia de Programação Dinâmica (ou Dynamic Programming (DP), em inglês) é evitar o recálculo de uma função para os mesmos parâmetros que já calculamos alguma vez, salvando todos os resultados já obtidos até então e calculando o valor da função apenas se ele nunca foi calculado, exatamente como fizemos no exemplo da sequência de Fibonacci. Assim só calculamos cada valor da função uma única vez!

em geral o que queremos com DP é: contar, calcular o máximo/mínimo, saber se algo existe ou não, além de outras ocasiões menos comuns.
***
## Estados

Chamaremos de estados da DP os parâmetros que usamos para definir a função

### EX 1:

Temos uma escada com n degraus e um atleta, Pisano. Sabemos que, a partir degrau do i, Pisano consegue andar para o degrau i+1 ou i+2. Nessas condições queremos saber a quantidade de maneiras distintas que Pisano consegue chegar do primeiro até o último degrau (Duas maneiras são distintas se a quantidade de passos dados é diferente ou se existe algum i tal que o i-ésimo passo na primeira sequência é diferente do i-ésimo passo na segunda sequência).

Primeira possibilidade -> Poderíamos definir uma função cujo parâmetro é o conjunto de todos valores já visitados nesse caminho, o que seria uma função perfeitamente válida, especialmente se quiséssemos printar todos as possibilidades na tela. Esse método é comumente chamado de força bruta (ou _brute force_ em inglês), pois nós estamos simplesmente gerando todas as possibilidades. Segue uma implementação dessa ideia para melhor entendimento:

```c++
#include <cstdio>
#include <vector>
using namespace std;

int solve(vector<int> caminho, int n) {
    
    int atual = caminho.back(), ans = 0;

    if (atual + 1 <= n) {
        caminho.push_back(atual+1);
        ans += solve(caminho, n);
        caminho.pop_back();
    }

    if (atual + 2 <= n) {
        caminho.push_back(atual + 2);
        ans += solve(caminho, n);
        caminho.pop_back();
    }

    if (atual == n) ++ans;
    return ans;
}

int main() {
	int n; scanf("%d", &n);
	printf("%d\n", solve({1}, n));
}
``` 
***
Em geral, o que queremos ter em uma função da DP é encontrar um **conjunto de propriedades que nos permita agrupar vários casos em um único estado**, e o que precisamos garantir é que quaisquer dois casos que tenham as mesmas propriedades terão a mesma resposta para essa função.

### EX 1 OTIMIZADO COM DP:

```c++
#include <bits/stdc++.h>

using namespace std;

using namespace std;

const int maxn = 10010;

int dp[maxn];
bool mark[maxn];

int solve(int i, int n) {
    
     if (i == n) return 1;
     if (i > n) return 0;
     if (n == 0 || n == 1) return 0;
    
     if (mark[i]) return dp[i];
    
     dp[i] = solve(i + 1, n) + solve(i + 2, n);
     mark[i] = 1;   
     return dp[i];
}

int main() {
	int n; scanf("%d", &n);
	printf("%d\n", solve(0, n));
}
 
``` 
## Transição 

A transição de uma DP é o conjunto de possibilidades que temos que considerar para _transitar_ de um estado para o outro. Por exemplo no problema mostrado acima a transição era ir do estado F(i) para F(i+1) ou F(i+2).