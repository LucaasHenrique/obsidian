***
**Criado em**: 2025-09-21  
**Modificado em**: 20:27
**Topico**: #
***
>  Quando analisamos assintoticamente um programa, nós nos preocupamos apenas com como o custo do programa varia a medida que sua entrada cresce, isso pode parecer meio simplista, por exemplo um programa que custa 1000⋅log(n) operações parece muito pior que um que custa n para um n pequeno, mas a medida que n cresce, o segundo algoritmos gasta bem mais tempo que o primeiro (para n=106, o primeiro consome em torno de 20000 operações, enquanto o segundo vai consumir 1000000 de operações), assim vemos que é uma forma válida de análise.
***

**O(1)** -> Um algoritmo que sempre vai demorar a mesma quantidade de tempo, 
independente da entrada, ou seja, de tempo constante.

```c++
cin >> a >> b;
c = a + b;
cout << c;
```
***

**O(log(n))** -> Esse algoritmo custa uma quantidade de operações proporcional ao logaritmo do número, assim se elevamos n ao quadrado, duplicamos o tempo necessário para o algoritmo gerar resposta, o algoritmo mais conhecido nessa complexidade é a busca binária, e o mais simples é tirar a parte inteira do logaritmo de um número.

```c++
//busca nos dígitos binários do número
//não é uma busca binária
//imprime a parte inteira da raiz de n
int n, sq = 0, test;
cin >> n;
for(int pot = 31; pot >= 0; --pot){
  test = sq + (1 << test);
  if(test*test <= n)  sq = test;
}
cout << sq << "\n"; 
```
***
**O(√n)** -> Um algoritmo que cresce como a raiz do próprio n, assim se multiplicamos n por quatro, esse programa demora 2 vezes a mais que antes.
```c++
// calcula a parte inteira da raiz de n
int n, sq;
cin >> n;
for(sq = 1; sq*sq <= n; ++sq);
--sq;
cout << sq << "\n";
```
****
**O(n)** -> Conhecido como linear. Geralmente um loop que vai de 0 a algum múltiplo fixo de n.
```c++
cin >> n;
for(int i = 0; i < n; ++i){
  cin >> x[i];
}
```
***
**O(n⋅log(n))** -> Os algoritmos primeiramente encontrados nessa categoria são as ordenações rápidas por comparação (quicksort, merge-sort, etc).
```c++
//ordenação usando a STL
int n, v[100000];
cin >> n;
for(int i = 0; i < n; ++i){  
  cin >> v[i]; //custa O(n)
}
sort(v, v + n); //ordena o vetor, custa O(nlog(n))
//n + nlog(n) = O(nlog(n))
```
***
**O(n²)** -> Conhecidos como algotitmos quadráticos, o programa demora tempo proporcional ao quadrado do n. Dessa forma se duplicamos o n, o tempo fica quatro vezes maior. Qualquer código que tenha que ler/preencher uma matriz quadrado de dimensão n custo pelo menos isso.

```c++
//ler as entradas de uma matriz
int n, G[1000][1000];
for(int i = 0; i < n; ++i){ //Temos O(n*custo do for interno)
  for(int j = 0; j < n; ++j){ //Termos O(n*operação do for)
    cin >> G[i][j]; //O(1)
  }
}    
//Assim a complexidade é O(n*O(n*(O(1)))) = O(n^2)
```
****
**O(2^n)** -> Conhecida como classe exponencial, os algoritmos dessa classe geralmente são força bruta.  Normalmente esses algoritmos têm que percorrer todos os subconjuntos de um conjunto de n elementos.
```c++
//Soma de conjunto, O(n*2^n)
int n, v[20], m;
cin >> n >> m;
for(int i = 0; i < n; ++i){
 cin >> v[i]; //leitura, O(n) 
}
for(int mask = 0; mask < (1 << n); ++mask){ //passa por todos os subconjuntos O(2^n)
  int soma = 0;
  for(int i = 0; i < n; ++i){ //loop O(n)
    if((1 << i)&mask){ //checa se um elemento está nesse subconjunto
      soma += v[i];
    }
  }
  if(m == soma){
    for(int i = 0; i < n; ++i){
      if((1 << i)&mask){
        cout << i << " ";
      }
    }
    cout << "\n";
    break;
  }
}
```
****
**O(n!)** -> Algoritmos que rodam em tempo proporcional ao fatorial, normalmente algoritmos dessa classe são força bruta. Um exemplo é o cacheiro viajante por força bruta.
```c++
//Checar a posição lexicogŕafica de uma ordem de um vetor, O(n * n!)
int n, v[10], u[10], ans, stop;
cin >> n;
for(int i = 0; i < n; ++i){
   cin >> v[i]; //leitura, O(n)
} 
for(int i = 0; i < n; ++i){
  u[i] = v[i]; //copio o vetor para outro, O(n)
}
sort(u, u + n) //ordenação, O(nlog(n))
for(ans = 0; 1; ++ans){
  stop = 0;
  for(int i = 0; i < n; ++i){ //checa se os vetores são iguais, O(n)
    if(u[i] != v[i])  break;
    if(i == n - 1)  stop = 1; 
  }
  if(stop){
     break;
  } 
  next_permutation(u, u + n); //transforma o u na próxima ordenação do vetor na ordem lexicográfica, pode se repetir n! vezes
}
cout << ans << "\n";;
```
