***
**Criado em**: 2025-09-20  
**Modificado em**: 16:08
**Topico**: #
***
## Formula geral para calcular o array P (prefix sum) de forma eficiente é: 

```c++
P[i] = P[i−1]+A[i]
```

A = [2, 4, 1, 7, 5]

sendo P[0] = A[0]

- `P[0] = 2`
- `P[1] = P[0] + A[1] = 2 + 4 = 6`
- `P[2] = P[1] + A[2] = 6 + 1 = 7`
- `P[3] = P[2] + A[3] = 7 + 7 = 14`    
- `P[4] = P[3] + A[4] = 14 + 5 = 19`
***

Um subarray arr[l..r] tem soma k se:

```p[r+1] - p[l] = k```

ou seja

```p[r+1] - k = p[l] ```

Então, para cada prefixo p[r+1], basta ver quantos prefixos p[l] já vimos que valem p[r+1] - k

```c++
int countSubarrays(vector<int>& arr, int k) {
    unordered_map<int, int> freq; 
    freq[0] = 1;  // prefixo vazio conta como p[0]

    int count = 0;
    int prefix = 0; // <- aqui começa o p[r+1]

    for (int x : arr) {
        prefix += x;   // agora prefix = p[r+1]
        
        // verificamos se já vimos algum p[l] = prefix - k
        if (freq.find(prefix - k) != freq.end()) {
            count += freq[prefix - k];
        }
        
        // registramos que vimos esse prefixo
        freq[prefix]++;
    }

    return count;
}
```
***
prefix sum
```c++
int n; cin >> n;
vector<int> a(n), p(n);
for (int& i: a) cin >> i;

p[0] = p[0];
for (int i = 1; i <= n; i++) p[i] = p[i-1] + a[i];

int q; cin >> q;

while (q--) {
	int l, r; cin >> l >> r;
	l--, r--;
	int ans = p[r];
	if (l > 0) ans -= p[l-1];
	cout << ans << endl;
}
``` 
