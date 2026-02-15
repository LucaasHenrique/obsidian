***
**Criado em**: 2026-02-04  
**Modificado em**: 07:06
**Topico**: #
***
# 1 - Fatorial - Beecrowd 
Answer - Sabendo que impossivel calcular fatorial em tempo suficiente. A resposta consiste em apenas pre-calcular todos os fatoriais menor que n, ou sabendo que n é ate 10⁵ podemos pegar um numero que o fatorial estoure o limite, como o 10! = 3628800. Assimo percorremos o vetor de final ao inicio é verificamos se o numero fatorial calculado é menor que n, se sim fazemos n -= fat[i];

se n = 25 -> 25 = 24(4!) + 1(1!);

```cpp
vector<int> fat(11);
fat[0] = 1;

for (int i = 1; i <= 10; i++) fat[i] = fat[i-1] * i;

int ans = 0;
for (size_t i = 10; i > 0; i--) {
	if (fat[i] <= n) {
		n -= fat[i];
		ans++;
		i++;
	} 
}
```
Complexidade O(1), i é constante, a operação de subtração tbm é constante;
***
# 2 - Phoenix and Balance - CF
answer -> Para uma possivel solução podemos pensar em juntar o maior valor com os menores possiveis é o segundo maior com os valores maiores que o ultimo valor escolhido pelo primeiro. 

```cpp
vector<int> a(n);
a[0] = 2;
for (int i = 1; i < n; i++) a[i] = a[i-1] * 2;

int p1 = a[n-1], p2 = a[n - 2], i = 0, j = n - 3;

while (i < j) {
   p1 += a[i]; p2 += a[j];
   i++; j--;
}
``` 
como o maior e segundo maior ja foram escolhidos o loop escolhe no maximo ((n - 2) / 2) valores para cada ponteiro.
***
# 3 - Road to zero - CF
tenho um (x, y) e preciso que ambas se tornem 0; ex: (1, 3) -> (0, 0)
posso fazer duas escolhas:
	a -> escolher um dos dois e aumentar ou diminuir 1
		custa a$
	b -> aumentar ou diminuir 2 em ambos
		custa b$

answer -> podemos pensar como uma reta numerica começando do 0 é indo ate x + y, ou seja é para isso podemos andar 1 ou 2 de distancia.

podemos assumir que um dos valores é maior, por exemplo: y >= x
nesse temos dois casos: 
	1 -> a + a <= b entao fazemos (x + y) * a
	2 -> a + a > b entao fazemos (x * b) + (y - x) * a

no primeiro caso queremos se saber se vale mais a pena andar 1  posição duas vezes escolhendo o custo de `2a` ou andar 2 posições de uma vez escolhendo o custo de `b`.

no segundo, como supomos que x é menor igual a b, significa que andamos 2 posições 2 x vezes a custo b, mais a distancia restante ate `y` com custo a;

```c++
void solve() {  
    ll x, y, a, b; cin >> x >> y >> a >> b;
    
    b = min(b, a + a);
    if (x < y) {
        int aux = y;
        y = x;
        x = aux;
    }
    cout << y * b + (x - y) * a << "\n";
}
``` 
***
# 4 - 1368A C+= - CF
answer: posso sempre crescer o menor valor com a soma a + b;

se a > b; eu faço b += a;
se b > a; eu faço a += b;

ou seja,  o codigo sempre vai intercalando fazendo uma hora `a` ser o maior e outra o `b`

é facil ver que essa é uma escolha gulosa
```c++
int sum = 0;
    int c = 0;
    while (sum <= n) {
        if (a > b) {
            b += a; sum = b;
        } else {
            a += b; sum = a;
        }
        c++;

        if (sum > n) break;
    }
```
***
# 5 - Taxi 158B - CF
answer -> se é grupo de 4 ocupa 1 taxi, nos outros casos tente juntar o maximo de grupos de 1 com grupos de 3 possiveis, os grupos de 2 com outros grupos de 2, em alguns casos grupos de 2 com grupos de 1. Quanto mais grupos eu consigo juntar em um unico taxi, menor é o numero de taxis que preciso no total.

alias: g1 -> grupo de 1, g2 -> grupo de 2, g3 -> grupo de 3, g4 -> grupo de 4

step-by-step ->
total_taxi = 0;
`1` - conte quantos de grupos de n pessoas existem
`2` - total_taxi += total de g4 existentes
`3` - se g2 > 0; verifico quantos g2 posso juntar em um unico taxi.
`4` - se g1 & d3 > 0, o total de uniãos vai ser o min(g1, g3), EX: se g1 = 1 e g3 = 3, só posso juntar um g1 com um g3, o restante de g3 vai para taxis diferentes; se g1 = 3 e g3 = 3, posso juntar cada g1 e g3 em um unico taxi.
`5` - se g1 e g2 > 0;  
	5.1 - verifico quantos g2 posso formar com o total de g1, para isso basta fazer a divisão inteira de g1 por 2; EX: g1 = 6 e g2 = 2 -> g1 / 2 = 3, entao posso juntar dois g2 formados com os g2 originais, basicamento eu quero verificar se existem g2s suficientes para os g2s originais.
	5.2 - se não -> o total de combinações vai ser o min(g1, g2) pelo motivo de min(g1, g3);
`6`- no final somamos qualquer valor residual de grupos no total_taxi;

```c++
 int n; cin >> n;

    vector<int> a(n);
    
    int c = 0;
    int a1 = 0, a2 = 0, a3 = 0, a4 = 0;
    for (int i = 0; i <n; i++) {cin >> a[i];
        if (a[i] == 1) a1++;
        if (a[i] == 2) a2++;
        if (a[i] == 3) a3++;
        if (a[i] == 4) a4++;
    }
    
    c += a4; a4 = 0;
    if (a2 ) {
        int t = a2 >> 1; 
        c += t;
        a2 -= t * 2;
    }
    if (a1  && a3 ) {
        int minv = min(a1, a3);
        c += minv;
        a1 -= minv;
        a3 -= minv;
    }
    if (a1 && a2) {
        if (a2 <= a1>>1 && a1 >> 1) {
            c += a2;
            a1 -= a2*2;
            a2 -= a2;
        } else {
            int z = min(a1, a2);
            c += z;
            a1 -= z;
            a2 -= z;
        }
    }

	// verificar se sobrou algum grupo de 1
    int y = a1 / 4;
    c += y;
    a1 -= y*4;

    if (a1 < 4 && a1) {
        c+=1;
        a1 = 0;
    }

    c += a1 + a2 + a3 + a4; 
```
***
# 5 - Multiplication Dilema - CF
Possivel  Solução!!!!!!
um numero é especial se ele contem um digito não-zero no inicio e é seguido por não-zero numeros de zeros; EX: 30, 10000;

answer -> podemos pegar o resto de divisão entre o numero q não é especial e 10: `n % 10`, e com esse valor descobrimos o quanto falta para esse numero ser especial, EX: 17 -> 17 % 10 = 7; 17 - 7 = 10, 10 é um numero especial

se b for o numero não especial ->
- pegamos o resto da divisao por 10
- fazemos uma troca entre a e b
se a for o numero não especial ->
- apenas pegamos o resto da divisão por 10

```cpp
int a, b; cin >> a >> b;

    int aux = 0;
    if (b % 10) {
        aux = b % 10;
        int al = b;
        b = a;
        a = al;
    } else aux = a % 10;

    cout << a - aux << " x " << b << " + " << aux << " x " << b << "\n";
```
***
# Chat Order - CF
answer ->  a solução é apenas pecorrer o vetor de n-1 ate 0 é printando a[i] caso ele ainda nao tenha aparecido.

da pra usar um set ou vector como historico de aparição

```c++
void solve() {
    int n; cin >> n;
    vector<string> a(n);
    for (int i = 0; i < n; i++) cin >> a[i]; 
    
    set<string> log;
    for (int i = n-1; i >= 0; i--) {
        if (!log.count(a[i])) cout << a[i] << "\n";
        log.insert(a[i]);
    }
}
```
