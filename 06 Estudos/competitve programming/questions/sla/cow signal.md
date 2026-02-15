***
**Criado em**: 2025-10-21  
**Modificado em**: 21:51
**Topico**: #
***
Bessie and her cow friends are playing as their favorite cow superheroes. Of course, everyone knows that any self-respecting superhero needs a signal to call them to action. Bessie has drawn a special signal on a sheet of M×N paper (1≤M≤10,1≤N≤10), but this is too small, much too small! Bessie wants to amplify the signal so it is exactly K times bigger (1≤K≤10) in each direction.

The signal will consist only of the '.' and 'X' characters.

INPUT FORMAT (file cowsignal.in):
The first line of input contains M
, N, and K, separated by spaces.

The next M
lines each contain a length-N

string, collectively describing the picture of the signal.

OUTPUT FORMAT (file cowsignal.out):
You should output KM
lines, each with KN
characters, giving a picture of the enlarged signal.

SAMPLE INPUT:

5 4 2
XXX.
X..X
XXX.
X..X
XXX.

SAMPLE OUTPUT:

XXXXXX..
XXXXXX..
XX....XX
XX....XX
XXXXXX..
XXXXXX..
XX....XX
XX....XX
XXXXXX..
XXXXXX..
***
a solução consite em pecorrer em cada linha em um loop e pecorrer cada caractere em um loop e para cada caractere executar um loop do tamanho de K

```c++
    int M, N, K;
    cin >> M >> N >> K;
    string arr[1000];
    string c;

    for (int i = 0; i < M; i++) {
        cin >> arr[i];
    }

    for (int i = 0; i < M; i++) {
        string temp = "";
        for (int j = 0; j < N; j++) for (int l = 0; l < K; l++) temp+=arr[i][j];
        for (int j = 0; j < K; j++) c+=temp + '\n';
    } 
```