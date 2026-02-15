# Threads em Diferentes Linguagens de Programação

## Índice
- [JavaScript: Single-Threaded com Event Loop](#javascript-single-threaded-com-event-loop)
- [Python: GIL e Threading Limitado](#python-gil-e-threading-limitado)
- [Java: True Multi-Threading](#java-true-multi-threading)
- [C/C++: Controle Total](#cc-controle-total)
- [Go: Goroutines](#go-goroutines)
- [Rust: Segurança e Performance](#rust-segurança-e-performance)
- [C#: Threading Robusto](#c-threading-robusto)
- [Ruby: GIL Similar ao Python](#ruby-gil-similar-ao-python)
- [Comparação Geral](#comparação-geral)

---

## JavaScript: Single-Threaded com Event Loop

### Como Funciona

JavaScript (Node.js e navegadores) é **single-threaded** - executa código em uma única thread principal. Mas consegue ser altamente concorrente através do **Event Loop**.

### Modelo de Execução

```javascript
// JavaScript - Event Loop
console.log('1');

setTimeout(() => {
  console.log('2');
}, 0);

console.log('3');

// Output: 1, 3, 2
```

**Por que?**

```
Call Stack          Web APIs           Callback Queue
┌──────────┐       ┌──────────┐       ┌──────────┐
│ log('3') │       │setTimeout│       │          │
├──────────┤       │  (timer) │       │          │
│ setTimeout│  →   └──────────┘       │          │
├──────────┤                          │          │
│ log('1') │       Após timer:        │ log('2') │
└──────────┘       ┌──────────┐       └──────────┘
                   │ Completo │  →    Move para queue
                   └──────────┘
```

### Event Loop

1. **Executa código síncrono** na Call Stack
2. **Operações assíncronas** (setTimeout, fetch, fs.readFile) vão para Web APIs
3. Quando completam, callbacks vão para **Callback Queue**
4. **Event Loop** monitora: se Call Stack está vazia, pega callbacks da queue

### Concorrência sem Paralelismo

```javascript
// Servidor HTTP - 1 thread atendendo milhares de conexões
const http = require('http');

http.createServer((req, res) => {
  // Operação de I/O (não bloqueia a thread)
  fs.readFile('arquivo.txt', (err, data) => {
    res.end(data);
  });
  // Thread continua livre para aceitar outras requisições
}).listen(3000);
```

**Como atende múltiplas requisições com 1 thread?**

- Requisição 1 chega → inicia leitura de arquivo → **não espera** → thread livre
- Requisição 2 chega → processa → thread livre
- Arquivo de Req 1 pronto → callback executado
- Tudo intercalado na mesma thread!

### Web Workers (quando precisa de threads)

```javascript
// main.js (thread principal)
const worker = new Worker('worker.js');

worker.postMessage({ numbers: [1, 2, 3, 4, 5] });

worker.onmessage = (e) => {
  console.log('Resultado:', e.data); // 15
};

// worker.js (thread separada!)
onmessage = (e) => {
  const sum = e.data.numbers.reduce((a, b) => a + b, 0);
  postMessage(sum);
};
```

**Limitações dos Web Workers:**
- Não compartilham memória (comunicação por mensagens)
- Não têm acesso ao DOM
- Overhead de criação

### Por que JavaScript é single-threaded?

1. **Histórico**: Criado para navegadores, manipular DOM é mais seguro com 1 thread
2. **Simplicidade**: Evita race conditions, locks, deadlocks
3. **Suficiente**: A maioria das tarefas web é I/O-bound, não CPU-bound

### Quando JavaScript sofre?

```javascript
// Cálculo pesado BLOQUEIA tudo
function fibonacci(n) {
  if (n <= 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
}

console.log('Início');
fibonacci(45); // TRAVA A APLICAÇÃO POR SEGUNDOS
console.log('Fim'); // Só executa depois
```

**Solução**: Usar Web Workers ou dividir o trabalho com `setImmediate`/`process.nextTick`.

---

## Python: GIL e Threading Limitado

### Global Interpreter Lock (GIL)

Python tem threads, mas o **GIL** (Global Interpreter Lock) permite que apenas **1 thread execute bytecode Python por vez**, mesmo com múltiplos núcleos.

### Como Funciona

```python
import threading

counter = 0

def increment():
    global counter
    for _ in range(1000000):
        counter += 1

# Criando 2 threads
t1 = threading.Thread(target=increment)
t2 = threading.Thread(target=increment)

t1.start()
t2.start()
t1.join()
t2.join()

print(counter)  # Esperado: 2000000, Real: ~1000000-1900000
```

**Por que o resultado está errado?**

O GIL alterna entre threads, mas `counter += 1` não é atômico:
1. Ler counter
2. Incrementar
3. Escrever counter

Thread 1 e 2 podem intercalar esses passos, causando race condition.

### GIL em Ação

```
Tempo →
Thread 1: [adquire GIL][executa bytecode][libera GIL]----[adquire GIL][executa]...
Thread 2: ------------------------------------[adquire GIL][executa][libera]-------...

Apenas 1 thread executa Python por vez!
```

### Quando Threading em Python Funciona Bem

**I/O-bound**: GIL é liberado durante operações de I/O!

```python
import threading
import requests

def download(url):
    # Durante o download, GIL é LIBERADO
    response = requests.get(url)
    print(f'Downloaded {len(response.content)} bytes')

urls = ['url1', 'url2', 'url3', 'url4']
threads = [threading.Thread(target=download, args=(url,)) for url in urls]

for t in threads:
    t.start()
for t in threads:
    t.join()

# Isso É MAIS RÁPIDO que sequencial!
```

### Quando Threading em Python NÃO Funciona

**CPU-bound**: GIL trava tudo.

```python
import threading
import time

def cpu_intensive():
    total = 0
    for i in range(10**7):
        total += i * i
    return total

# Com threads
start = time.time()
threads = [threading.Thread(target=cpu_intensive) for _ in range(4)]
for t in threads:
    t.start()
for t in threads:
    t.join()
print(f'Com threads: {time.time() - start}s')  # ~8s em 4 núcleos

# Sequencial
start = time.time()
for _ in range(4):
    cpu_intensive()
print(f'Sequencial: {time.time() - start}s')  # ~8s também!

# Threading NÃO AJUDA em CPU-bound por causa do GIL!
```

### Solução: Multiprocessing

```python
from multiprocessing import Process, Pool

def cpu_intensive(n):
    total = 0
    for i in range(n):
        total += i * i
    return total

# Cada processo tem seu próprio interpretador e GIL
with Pool(4) as pool:
    results = pool.map(cpu_intensive, [10**7, 10**7, 10**7, 10**7])

# Agora SIM usa múltiplos núcleos! ~2s em 4 núcleos
```

**Diferença**:
- **Threading**: Múltiplas threads, 1 processo, 1 GIL (bom para I/O)
- **Multiprocessing**: Múltiplos processos, cada um com seu GIL (bom para CPU)

### Por que Python tem GIL?

1. **Simplicidade**: Gerenciamento de memória mais simples
2. **C Extensions**: Muitas bibliotecas C não são thread-safe
3. **Histórico**: Decisão de design antiga difícil de remover

---

## Java: True Multi-Threading

### Threads Nativas

Java tem **threading verdadeiro** - cada thread Java mapeia para uma thread do SO (1:1). Sem GIL.

```java
public class MultiThreadExample {
    private static int counter = 0;
    
    public static void main(String[] args) throws InterruptedException {
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000000; i++) {
                counter++; // RACE CONDITION!
            }
        });
        
        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000000; i++) {
                counter++;
            }
        });
        
        t1.start();
        t2.start();
        t1.join();
        t2.join();
        
        System.out.println(counter); // Resultado imprevisível!
    }
}
```

### Sincronização

```java
public class SafeCounter {
    private int counter = 0;
    
    // synchronized garante que apenas 1 thread executa por vez
    public synchronized void increment() {
        counter++;
    }
    
    // Ou usando Lock explícito
    private Lock lock = new ReentrantLock();
    
    public void incrementWithLock() {
        lock.lock();
        try {
            counter++;
        } finally {
            lock.unlock();
        }
    }
}
```

### Thread Pools

```java
ExecutorService executor = Executors.newFixedThreadPool(4);

for (int i = 0; i < 100; i++) {
    final int taskId = i;
    executor.submit(() -> {
        System.out.println("Task " + taskId + " on " + 
                          Thread.currentThread().getName());
    });
}

executor.shutdown();
```

### Paralelismo Real em CPU-bound

```java
// Processamento paralelo de imagem
int cores = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(cores);

List<Future<BufferedImage>> futures = new ArrayList<>();
for (int i = 0; i < imageHeight; i += chunkSize) {
    final int startRow = i;
    futures.add(executor.submit(() -> processChunk(image, startRow)));
}

// Realmente usa múltiplos núcleos simultaneamente!
```

### Vantagens de Java

- ✅ Paralelismo real em múltiplos núcleos
- ✅ APIs robustas (java.util.concurrent)
- ✅ Thread pools, locks, semáforos, barreiras

### Desvantagens

- ❌ Gerenciamento manual de sincronização
- ❌ Fácil ter race conditions e deadlocks
- ❌ Threads pesadas (cada uma consome memória)

---

## C/C++: Controle Total

### Threads POSIX (pthreads)

```c
#include <pthread.h>
#include <stdio.h>

void* thread_function(void* arg) {
    int id = *(int*)arg;
    printf("Thread %d executando\n", id);
    return NULL;
}

int main() {
    pthread_t threads[4];
    int ids[4] = {1, 2, 3, 4};
    
    for (int i = 0; i < 4; i++) {
        pthread_create(&threads[i], NULL, thread_function, &ids[i]);
    }
    
    for (int i = 0; i < 4; i++) {
        pthread_join(threads[i], NULL);
    }
    
    return 0;
}
```

### C++11 Threading

```cpp
#include <thread>
#include <mutex>
#include <iostream>

std::mutex mtx;
int counter = 0;

void increment(int n) {
    for (int i = 0; i < n; i++) {
        std::lock_guard<std::mutex> lock(mtx);
        counter++;
    }
}

int main() {
    std::thread t1(increment, 1000000);
    std::thread t2(increment, 1000000);
    
    t1.join();
    t2.join();
    
    std::cout << counter << std::endl; // 2000000 (correto!)
    return 0;
}
```

### Operações Atômicas

```cpp
#include <atomic>

std::atomic<int> counter(0);

void increment() {
    for (int i = 0; i < 1000000; i++) {
        counter++; // Atômico! Sem mutex necessário
    }
}
```

### Performance Máxima

C/C++ permite:
- Threads extremamente leves
- Controle fino de afinidade de CPU
- Lock-free programming
- SIMD manual

```cpp
// Definir em qual núcleo a thread executa
cpu_set_t cpuset;
CPU_ZERO(&cpuset);
CPU_SET(2, &cpuset); // Núcleo 2
pthread_setaffinity_np(thread, sizeof(cpu_set_t), &cpuset);
```

---

## Go: Goroutines

### Modelo Único: M:N Threading

Go usa **goroutines** - threads leves gerenciadas pelo runtime. Milhares de goroutines mapeadas para poucas threads do SO.

```go
package main

import (
    "fmt"
    "time"
)

func say(s string) {
    for i := 0; i < 5; i++ {
        time.Sleep(100 * time.Millisecond)
        fmt.Println(s)
    }
}

func main() {
    go say("world") // Cria goroutine
    say("hello")
}
```

### Como Funciona

```
Goroutines (milhares):    g1, g2, g3, g4, g5, ..., g1000
                           ↓   ↓   ↓   ↓   ↓        ↓
Threads do SO (poucas):   [T1] [T2] [T3] [T4]
                           ↓    ↓    ↓    ↓
Núcleos da CPU:           [C1] [C2] [C3] [C4]
```

O **scheduler do Go** multiplexa goroutines sobre threads do SO.

### Goroutines são Baratas

```go
func main() {
    for i := 0; i < 100000; i++ {
        go func(n int) {
            // Cada goroutine usa ~2KB de stack
            time.Sleep(time.Hour)
        }(i)
    }
    time.Sleep(time.Hour)
}

// 100.000 goroutines = ~200MB
// 100.000 threads do SO = CRASH (cada thread ~1-8MB)
```

### Channels: Comunicação Segura

```go
func worker(id int, jobs <-chan int, results chan<- int) {
    for j := range jobs {
        fmt.Printf("Worker %d processando job %d\n", id, j)
        results <- j * 2
    }
}

func main() {
    jobs := make(chan int, 100)
    results := make(chan int, 100)
    
    // 3 workers paralelos
    for w := 1; w <= 3; w++ {
        go worker(w, jobs, results)
    }
    
    // Enviar 5 jobs
    for j := 1; j <= 5; j++ {
        jobs <- j
    }
    close(jobs)
    
    // Receber resultados
    for a := 1; a <= 5; a++ {
        <-results
    }
}
```

### Filosofia: "Don't communicate by sharing memory; share memory by communicating"

---

## Rust: Segurança e Performance

### Ownership e Threading

Rust **garante em compile-time** que não há race conditions!

```rust
use std::thread;

fn main() {
    let v = vec![1, 2, 3];
    
    let handle = thread::spawn(|| {
        println!("{:?}", v); // ERRO DE COMPILAÇÃO!
        // v pode ter sido desalocado
    });
    
    handle.join().unwrap();
}
```

**Correção**: Transferir ownership

```rust
let v = vec![1, 2, 3];

let handle = thread::spawn(move || {
    println!("{:?}", v); // OK! v foi movido para a thread
});

// println!("{:?}", v); // ERRO! v não existe mais aqui
```

### Compartilhamento Seguro

```rust
use std::sync::{Arc, Mutex};
use std::thread;

fn main() {
    let counter = Arc::new(Mutex::new(0)); // Arc = Atomic Reference Count
    let mut handles = vec![];
    
    for _ in 0..10 {
        let counter = Arc::clone(&counter);
        let handle = thread::spawn(move || {
            let mut num = counter.lock().unwrap();
            *num += 1;
        });
        handles.push(handle);
    }
    
    for handle in handles {
        handle.join().unwrap();
    }
    
    println!("Result: {}", *counter.lock().unwrap()); // 10 (sempre!)
}
```

### Vantagens

- ✅ Segurança em compile-time (impossível ter data races)
- ✅ Performance de C/C++
- ✅ Zero-cost abstractions

---

## C#: Threading Robusto

### Tasks e async/await

```csharp
using System;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // Inicia 3 tasks paralelas
        Task<int> task1 = CalculateAsync(10);
        Task<int> task2 = CalculateAsync(20);
        Task<int> task3 = CalculateAsync(30);
        
        // Aguarda todas
        int[] results = await Task.WhenAll(task1, task2, task3);
        
        Console.WriteLine($"Sum: {results.Sum()}");
    }
    
    static async Task<int> CalculateAsync(int n)
    {
        await Task.Delay(1000); // Simula trabalho
        return n * n;
    }
}
```

### Parallel.For

```csharp
// Processamento paralelo automático
int[] numbers = Enumerable.Range(0, 1000000).ToArray();
int[] results = new int[numbers.Length];

Parallel.For(0, numbers.Length, i =>
{
    results[i] = numbers[i] * numbers[i];
});

// .NET automaticamente distribui entre núcleos
```

### PLINQ

```csharp
var numbers = Enumerable.Range(0, 10000000);

// Paralelo automático
var primes = numbers
    .AsParallel()
    .Where(n => IsPrime(n))
    .ToArray();
```

---

## Ruby: GIL Similar ao Python

Ruby também tem GIL (em MRI/CRuby):

```ruby
require 'thread'

counter = 0
threads = []

10.times do
  threads << Thread.new do
    1000000.times { counter += 1 }
  end
end

threads.each(&:join)
puts counter # Resultado incorreto por race condition
```

**Solução**: Usar processos (fork) ou JRuby/Rubinius que não têm GIL.

---

## Comparação Geral

| Linguagem | Modelo | Paralelismo Real? | Melhor Para |
|-----------|--------|-------------------|-------------|
| **JavaScript** | Single-thread + Event Loop | ❌ (exceto Workers) | I/O pesado, web servers |
| **Python** | Threading com GIL | ❌ (só multiprocessing) | Scripts, I/O, data science |
| **Java** | Threads nativas 1:1 | ✅ | Aplicações enterprise, servidores |
| **C/C++** | Controle total | ✅ | Performance crítica, sistemas |
| **Go** | Goroutines M:N | ✅ | Servidores, microserviços, concorrência |
| **Rust** | Threads seguras | ✅ | Sistemas, performance + segurança |
| **C#** | Tasks + async/await | ✅ | Windows apps, jogos (Unity), enterprise |
| **Ruby** | Threading com GIL | ❌ | Web apps (Rails), scripting |

---

## Resumo por Tipo de Tarefa

### I/O-Bound (rede, disco, banco de dados)

**Melhores**: JavaScript, Python (threading), Go (goroutines), C# (async/await)

Não precisa de paralelismo real - concorrência assíncrona é suficiente.

### CPU-Bound (cálculos pesados, processamento)

**Melhores**: Java, C/C++, Go, Rust, Python (multiprocessing)

Precisa de paralelismo real em múltiplos núcleos.

### Facilidade vs Controle

```
Fácil/Seguro                              Difícil/Controle Total
    ↓                                            ↓
JavaScript → Go → C# → Java → Rust → C/C++
```

### Escolha Baseada no Problema

- **Web backend I/O pesado**: Node.js, Go, Python (async)
- **Processamento de dados**: Java, C++, Rust
- **Prototipagem rápida**: Python, Ruby
- **Sistemas críticos**: C, C++, Rust
- **Microsserviços**: Go, Java
- **Desktop apps**: C#, Java, C++

A escolha depende mais do problema que você está resolvendo do que da "melhor" linguagem!
