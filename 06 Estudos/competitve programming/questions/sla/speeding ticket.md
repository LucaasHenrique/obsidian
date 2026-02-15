***
**Criado em**: 2025-10-23  
**Modificado em**: 21:45
**Topico**: #
***
Always the troublemaker, Bessie the cow has stolen Farmer John's tractor and taken off down the road!

The road is exactly 100 miles long, and Bessie drives the entire length of the road before ultimately being pulled over by a police officer, who gives Bessie a ticket for exceeding the speed limit, for having an expired license, and for operating a motor vehicle while being a cow. While Bessie concedes that the last two tickets are probably valid, she questions whether the police officer was correct in issuing the speeding ticket, and she wants to determine for herself if she has indeed driven faster than the speed limit for part of her journey.

The road is divided into N
segments, each described by a positive integer length in miles, as well as an integer speed limit in the range 1…100 miles per hour. As the road is 100 miles long, the lengths of all N

segments add up to 100. For example, the road might start with a segment of length 45 miles, with speed limit 70, and then it might end with a segment of length 55 miles, with speed limit 60.

Bessie's journey can also be described by a series of segments, M
of them. During each segment, she travels for a certain positive integer number of miles, at a certain integer speed. For example, she might begin by traveling 50 miles at a speed of 65, then another 50 miles at a speed of 55. The lengths of all M

segments add to 100 total miles. Farmer John's tractor can drive 100 miles per hour at its fastest.

Given the information above, please determine the maximum amount over the speed limit that Bessie travels during any part of her journey.

INPUT FORMAT (file speeding.in):
The first line of the input contains N
and M, separated by a space.

The next N

lines each contain two integers describing a road segment, giving its length and speed limit.

The next M

lines each contain two integers describing a segment in Bessie's journey, giving the length and also the speed at which Bessie was driving.

OUTPUT FORMAT (file speeding.out):
Please output a single line containing the maximum amount over the speed limit Bessie drove during any part of her journey. If she never exceeds the speed limit, please output 0.

SAMPLE INPUT:

3 3
40 75
50 35
10 45
40 76
20 30
40 40

SAMPLE OUTPUT:
5
***
the solution consists of declaring a vector from 0 to 100 indices representing each mile travelad. Each mile has a speed limit.

a solução  consiste em declarar um vetor de 0 a 100 indices representando cada milha viajada. Cada milha possui um limite de velocidade

Ou seja, caso na viajem de bessie ela esteja com uma velocidade acima do permitodo em determinado um inidice **i** fazemos um ```max(y-arr[it+j])``` para pegar a maior quantidade acima do limite permitido.

```c++
#include <bits/stdc++.h>

using namespace std;

#define range(it, a, b) for (ll it = a; it < b; it++)
#define all(x) begin(x), end(x)
#define ll long long
#define ull unsigned long long
#define INF64 ((ll) 1 << 60)
#define INF32 (1 << 30)

int n, m, ans;
int arr[105];

int main (int argc, char *argv[]) {
    
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    
    /*freopen("speeding.in", "r", stdin);
    freopen("speeding.out", "w", stdout);*/
    
    cin >> n >> m;

    int it = 0;
    for (int i = 0; i < n; i++) {
        int x, y; cin >> x >> y; 
        for (int j = 0; j < x; j++) arr[it+j] = y;
        it += x;
    }
    
    it = 0;
    for (int i = 0; i < m; i++) {
        int x, y; cin >> x >> y;
        for (int j = 0; j < x; j++) ans = max(ans, y-arr[it+j]);
        it += x;
    }

    cout << ans;

    return 0;
}
```