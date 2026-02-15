***
**Criado em**: 2026-02-10  
**Modificado em**: 06:22
**Topico**: #
***
# 1 - Bad Prices - CF
int mn = INF32
answer -> percorrendo o array da posição `n - 1` ate `0` pegamos o minimo entre `a[i]` e `mn` -> `mn = min(a[i], mn)` sempre que a[i] > mn, a[i] é um bad price.

```cpp
int n; cin >> n;
    
vector<int> a(n);
for (int i = 0; i < n; i++) cin >> a[i];

int c = 0;
int mn = INF32;
for (int i = n-1; i >= 0; i--) {
	mn = min(a[i], mn);
	if (a[i] > mn) {
		c++;
	}
}
``` 
