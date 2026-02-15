---
id: greedy algorithm
aliases: []
tags: []
---
***
**Criado em**: 2025-09-23  
**Modificado em**: 16:59
**Topico**: #
***
## O que é? 

-> 
Um algoritmo guloso (greedy algorithm) é uma técnica de resolução de problemas onde se toma a melhor decisão local em cada passo, esperando que isso leve à solução global ótima.

Ou seja, ele não revisita decisões anteriores: escolhe sempre a "melhor opção no momento" e segue adiante.

**Quando funciona:**

- O problema precisa ter **propriedade gulosa** (a escolha local ótima leva à solução global ótima).
- O problema deve ter **subestrutura ótima** (uma solução ótima pode ser construída a partir de soluções ótimas de subproblemas).

-> Um problema tem **subestrutura ótima** quando a **solução ótima do problema inteiro pode ser construída a partir de soluções ótimas de subproblemas menores**

**Quando não funciona:**
- Nem sempre decisões locais ótimas levam à solução global ótima.
---


## EX: 

> Imagine o seguinte problema: você é o dono de uma grande rede de postos de gasolina e, ao final do mês, você renova seu estoque. Nesse dia, o setor de pesquisa da sua empresa lhe envia uma lista com os preços e estoques dos seus maiores fornecedores. A primeira linha da lista tem um inteiros **n** e um decimal **d**, o número de fornecedores e a demanda do mercado, respectivamente. Cada uma das próximas **n** linhas tem dois decimais: **pi** e **ei**, respectivamente. Na i-ésima linha, **pi** é o preço do litro de gasolina no fornecedor *i* e *pi* é o estoque desse fornecedor em litros. Você deseja comprar exatamente a demanda que precisa (para que seu lucro seja máximo pela lei da oferta e da procura), então faça um programa que calcule quanto dinheiro você irá gastar nessa compra de modo que o custo seja mínimo, e imprima esse valor com precisão de duas casas decimais. Se não houver estoque suficiente no mercado para a sua compra, imprima uma única linha com a palavra “Impossivel”.

propriedade gulosa -> Escolher **sempre o fornecedor mais barato primeiro** garante o custo mínimo, pois qualquer outra escolha resultaria em pagar mais caro por algum litro.

```c++
#include <bits/stdc++.h>

using namespace std;

struct gas {
    double preco;
    double estoq;
};

bool compara(gas x, gas y) {return x.preco < y.preco; }

int main (int argc, char *argv[]) {
   
    int n; 
    double d;

    cin >> n >> d;
    double custo;
    vector<gas> forn;

    for (int i = 0; i < n; i++) {
        double x, y; cin >> x >> y;
        forn.push_back({x, y}); 
    }

    sort(forn.begin(), forn.end(), compara);

    for (int i = 0; i < n; i++) {
        gas davez = forn[i];

        if (davez.estoq < d) {
            custo += davez.estoq * davez.preco;
            d -= davez.estoq;
        } else {
            custo += 
            d = 0;
            break;
        }
    }

    if (d) cout << "impossivel" << "\n";
    else cout << custo << "\n";

    return 0;
}
```

## EX:

> O dentista quer sempre atender à consulta que conflitua com o menor número de consultas que ele ainda pode pegar. Como ordenar, então as escolhas? Parece bem atrativo escolhermos sempre as consultas de menor duração que não conflituam com as já escolhidas, mas veja o seguinte caso: tenho uma consulta que começa às 9 e termina às 12 (três horas de duração), uma que começa às 11 e termina às 13 (duas horas de duração) e uma que começa às 12 e termina às 15 (três horas de duração). Note que é melhor escolher as duas consultas mais longas do que escolher a curta, pois elas são conflitantes. Ponha-se então no lugar do dentista: você acabou de atender um paciente e na sala de espera estão todas as pessoas cujo horário do começo da consulta ainda não passou, qual delas você atenderia? A que termina primeiro! Qualquer outra consulta que termine um pouco mais tarde pode acabar conflituando com alguma outra que você poderia atender se tivesse pego a consulta que termina mais cedo! Assim, faremos um guloso que ordena as consultas por fim e vamos sempre atender a consulta (que ainda pode ser atendida, ou seja, que não passou ainda o horário do começo) que termina mais cedo.

propriedade gulosa -> Sempre escolher a consulta que termina mais cedo entre as que podem ser atendidas.

```c++
#include <bits/stdc++.h>

using namespace std;

// compromisso
struct comp {
    int ini;
    int fim;
};

bool compara(comp a, comp b) {return a.fim < b.fim; }

int main (int argc, char *argv[]) {
        
    int n; cin >> n;
    vector<comp> c;
    int count = 0;

    for (int i = 0; i < n; i++) {
        int x, y; cin >> x >> y;
        c.push_back({x, y});
    }

    sort(c.begin(), c.end(), compara);

    int livre = 0;
    for (int i = 0; i < n; i++) {
        comp aux = c[i];

        if (aux.ini >= livre) {
            count++;
            livre = c[i].fim;
        }
    }

    cout << count << "\n";
    
    return 0;
}
```

































