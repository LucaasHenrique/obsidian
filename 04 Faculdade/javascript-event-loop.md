# Event Loop do JavaScript: Guia Completo

## Índice
- [O que é o Event Loop](#o-que-é-o-event-loop)
- [Arquitetura Completa](#arquitetura-completa)
- [Os Componentes](#os-componentes)
- [Como Funciona Passo a Passo](#como-funciona-passo-a-passo)
- [Tipos de Tarefas](#tipos-de-tarefas)
- [Exemplos Práticos](#exemplos-práticos)
- [Armadilhas Comuns](#armadilhas-comuns)
- [Event Loop no Node.js](#event-loop-no-nodejs)

---

## O que é o Event Loop

O **Event Loop** é o mecanismo que permite JavaScript executar operações não-bloqueantes (assíncronas) mesmo sendo **single-threaded** (uma única thread de execução).

### Analogia

Imagine um restaurante com **apenas 1 garçom** (single-thread):

**Sem Event Loop** (bloqueante):
```
1. Atende Mesa 1 → vai na cozinha → ESPERA o pedido ficar pronto (5min)
2. Volta com pedido → Atende Mesa 2 → vai na cozinha → ESPERA (5min)
3. Todas as mesas esperando muito tempo!
```

**Com Event Loop** (não-bloqueante):
```
1. Atende Mesa 1 → anota pedido → passa pra cozinha → VAI EMBORA
2. Atende Mesa 2 → anota pedido → passa pra cozinha → VAI EMBORA
3. Atende Mesa 3 → anota pedido
4. Cozinha avisa "Mesa 1 pronta!" → garçom entrega
5. Atende Mesa 4
6. Cozinha avisa "Mesa 2 pronta!" → garçom entrega
```

O garçom (thread) nunca fica parado esperando!

---

## Arquitetura Completa

```
┌───────────────────────────────────────────────┐
│            JavaScript Engine (V8)              │
│                                                │
│  ┌──────────────┐        ┌─────────────────┐  │
│  │  Call Stack  │        │  Heap (Memória) │  │
│  │              │        │                 │  │
│  │  função3()   │        │   objetos       │  │
│  │  função2()   │        │   arrays        │  │
│  │  função1()   │        │   etc...        │  │
│  └──────────────┘        └─────────────────┘  │
│                                                │
└────────────────┬───────────────────────────────┘
                 │
    ┌────────────┴────────────┐
    │                         │
┌───▼─────────┐         ┌────▼──────────┐
│  Web APIs   │         │  Event Loop   │
│  (Browser)  │         │               │
│             │         │  ┌─────────┐  │
│ setTimeout  │         │  │ Monitor │  │
│ fetch       │◄────────┤  │ Stack   │  │
│ DOM events  │         │  │ & Queue │  │
│ etc...      │         │  └─────────┘  │
└─────┬───────┘         └───────────────┘
      │                          ▲
      │  Callback pronto         │
      │                          │
      ▼                          │
┌─────────────────────────────────┴─────┐
│         Callback/Task Queue           │
│                                       │
│  [callback1] [callback2] [callback3]  │
│                                       │
└───────────────────────────────────────┘
      │
      │ Quando Call Stack vazia
      ▼
  Executa próximo callback
```

---

## Os Componentes

### 1. Call Stack (Pilha de Chamadas)

Onde o JavaScript **executa** o código. É uma estrutura **LIFO** (Last In, First Out).

```javascript
function multiply(a, b) {
    return a * b;
}

function square(n) {
    return multiply(n, n);
}

function printSquare(n) {
    const result = square(n);
    console.log(result);
}

printSquare(4);
```

**Evolução da Call Stack:**

```
1. Início:
   Call Stack: []

2. printSquare(4) é chamada:
   Call Stack: [printSquare]

3. square(4) é chamada dentro de printSquare:
   Call Stack: [printSquare, square]

4. multiply(4, 4) é chamada dentro de square:
   Call Stack: [printSquare, square, multiply]

5. multiply retorna 16:
   Call Stack: [printSquare, square]

6. square retorna 16:
   Call Stack: [printSquare]

7. console.log(16) é chamada:
   Call Stack: [printSquare, console.log]

8. console.log retorna:
   Call Stack: [printSquare]

9. printSquare retorna:
   Call Stack: []
```

### 2. Web APIs / Node APIs

Funcionalidades fornecidas pelo **ambiente** (navegador ou Node.js), não pelo JavaScript em si:

**No Navegador:**
- `setTimeout` / `setInterval`
- `fetch` (requisições HTTP)
- DOM Events (`addEventListener`)
- `XMLHttpRequest`
- `requestAnimationFrame`

**No Node.js:**
- `fs` (file system)
- `http` / `https`
- `crypto`
- `child_process`

Essas APIs executam **fora da thread principal** do JavaScript!

### 3. Callback Queue / Task Queue

Fila onde ficam os **callbacks** prontos para executar. É uma estrutura **FIFO** (First In, First Out).

```
Queue: [callback1] ← [callback2] ← [callback3]
       (próximo)                    (último)
```

### 4. Event Loop

O **monitor** que verifica constantemente:

```javascript
while (true) {
    if (callStack.isEmpty()) {
        if (callbackQueue.hasCallbacks()) {
            const callback = callbackQueue.dequeue();
            callStack.push(callback);
            execute(callback);
        }
    }
}
```

**Regra de ouro**: Event Loop **só move callbacks** da queue para a stack quando a stack está **completamente vazia**.

---

## Como Funciona Passo a Passo

### Exemplo Clássico

```javascript
console.log('1');

setTimeout(() => {
    console.log('2');
}, 0);

console.log('3');

// Output: 1, 3, 2
```

### Execução Detalhada

**Passo 1**: `console.log('1')` entra na Call Stack
```
Call Stack: [console.log('1')]
Output: "1"
```

**Passo 2**: `console.log('1')` termina e sai da stack
```
Call Stack: []
```

**Passo 3**: `setTimeout(...)` entra na Call Stack
```
Call Stack: [setTimeout]
```

**Passo 4**: `setTimeout` registra o callback na Web API e sai da stack
```
Call Stack: []
Web APIs: [Timer de 0ms com callback]
```

**Passo 5**: Timer completa instantaneamente, callback vai para a Queue
```
Call Stack: []
Callback Queue: [() => console.log('2')]
```

**Passo 6**: `console.log('3')` entra na Call Stack
```
Call Stack: [console.log('3')]
Callback Queue: [() => console.log('2')]
Output: "3"
```

**Passo 7**: `console.log('3')` sai da stack
```
Call Stack: []  ← VAZIA!
Callback Queue: [() => console.log('2')]
```

**Passo 8**: Event Loop detecta stack vazia, pega callback da queue
```
Call Stack: [() => console.log('2')]
Callback Queue: []
```

**Passo 9**: Callback executa
```
Call Stack: [console.log('2')]
Output: "2"
```

**Passo 10**: Tudo completo
```
Call Stack: []
Callback Queue: []
```

**Por isso o output é: 1, 3, 2**

---

## Tipos de Tarefas

### Macrotasks (Tasks)

Callbacks de:
- `setTimeout`
- `setInterval`
- `setImmediate` (Node.js)
- I/O operations
- UI rendering

### Microtasks

Callbacks de:
- `Promise.then/catch/finally`
- `process.nextTick` (Node.js)
- `MutationObserver`
- `queueMicrotask`

### Prioridade: Microtasks > Macrotasks

```javascript
console.log('1');

setTimeout(() => console.log('2'), 0);

Promise.resolve().then(() => console.log('3'));

console.log('4');

// Output: 1, 4, 3, 2
```

**Por quê?**

```
1. Call Stack executa código síncrono:
   console.log('1') → Output: "1"
   setTimeout registrado
   Promise registrado
   console.log('4') → Output: "4"

2. Call Stack vazia, Event Loop verifica:
   
   Microtask Queue: [() => console.log('3')]
   Macrotask Queue: [() => console.log('2')]
   
   Event Loop SEMPRE processa TODAS as microtasks primeiro!
   
3. Executa microtask:
   console.log('3') → Output: "3"
   
4. Microtask Queue vazia, pega macrotask:
   console.log('2') → Output: "2"
```

**Fluxo Completo:**

```
┌─────────────────────────┐
│   Executar script       │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│  Processar TODAS as     │◄──┐
│  Microtasks             │   │
└────────────┬────────────┘   │
             │                │
             ▼                │
┌─────────────────────────┐   │
│  Pegar UMA Macrotask    │   │
└────────────┬────────────┘   │
             │                │
             ▼                │
┌─────────────────────────┐   │
│  Render (se browser)    │   │
└────────────┬────────────┘   │
             │                │
             └────────────────┘
             (loop infinito)
```

---

## Exemplos Práticos

### Exemplo 1: setTimeout vs Promise

```javascript
setTimeout(() => console.log('timeout'), 0);

Promise.resolve()
    .then(() => console.log('promise1'))
    .then(() => console.log('promise2'));

console.log('sync');

// Output:
// sync
// promise1
// promise2
// timeout
```

**Explicação:**
1. `sync` - código síncrono primeiro
2. `promise1`, `promise2` - microtasks (prioridade)
3. `timeout` - macrotask (por último)

### Exemplo 2: Microtasks Infinitas

```javascript
console.log('start');

setTimeout(() => console.log('timeout'), 0);

Promise.resolve().then(function promiseLoop() {
    console.log('promise');
    Promise.resolve().then(promiseLoop); // Cria nova microtask!
});

console.log('end');

// Output:
// start
// end
// promise
// promise
// promise
// promise
// ... (infinito!)
```

**Por quê nunca chega no timeout?**

Event Loop processa **TODAS** as microtasks antes de pegar uma macrotask. Como sempre criamos uma nova microtask, a fila nunca esvazia!

### Exemplo 3: Fetch (Real World)

```javascript
console.log('1');

fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => console.log('Data:', data));

console.log('2');

// Output:
// 1
// 2
// Data: {...}
```

**Passo a Passo:**

```
1. console.log('1') → Output: "1"

2. fetch() inicia requisição HTTP
   Web APIs: [HTTP Request em andamento]
   
3. .then() registra callback (não executa ainda!)

4. console.log('2') → Output: "2"

5. Call Stack vazia, esperando...

6. (depois de alguns ms) HTTP completa
   Microtask Queue: [response => response.json()]
   
7. Event Loop pega microtask
   response.json() é processado
   
8. Outro .then() callback na microtask queue
   Microtask Queue: [data => console.log('Data:', data)]
   
9. Event Loop pega e executa
   Output: "Data: {...}"
```

### Exemplo 4: Event Listeners

```javascript
button.addEventListener('click', () => {
    console.log('Clicked!');
    
    Promise.resolve().then(() => console.log('Promise'));
    
    setTimeout(() => console.log('Timeout'), 0);
});

// Quando usuário clica:
// Output:
// Clicked!
// Promise
// Timeout
```

**Por quê essa ordem?**

1. Click handler vai pra macrotask queue
2. Event Loop pega e executa
3. Durante execução:
   - `console.log('Clicked!')` - síncrono
   - Promise callback → microtask queue
   - setTimeout callback → macrotask queue
4. Click handler termina
5. Event Loop processa microtask (Promise)
6. Depois processa próxima macrotask (setTimeout)

---

## Armadilhas Comuns

### 1. setTimeout não garante tempo exato

```javascript
setTimeout(() => console.log('Done'), 1000);

// Longo processamento
for (let i = 0; i < 1000000000; i++) {}

// "Done" vai demorar MAIS de 1 segundo!
```

**Por quê?**
- setTimeout de 1000ms coloca callback na queue **após** 1 segundo
- Mas Event Loop **só pega da queue quando Call Stack está vazia**
- Se o loop estiver executando, stack não fica vazia
- Callback espera na queue até o loop terminar

### 2. Blocking the Event Loop

```javascript
// MAU - bloqueia tudo
function calculateHeavy() {
    let sum = 0;
    for (let i = 0; i < 10000000000; i++) {
        sum += i;
    }
    return sum;
}

button.addEventListener('click', calculateHeavy);
// Clique trava a aplicação inteira!
```

**Solução 1: Dividir o trabalho**

```javascript
function calculateHeavyAsync() {
    let sum = 0;
    let i = 0;
    
    function chunk() {
        const end = Math.min(i + 10000000, 10000000000);
        for (; i < end; i++) {
            sum += i;
        }
        
        if (i < 10000000000) {
            setTimeout(chunk, 0); // Libera Event Loop
        } else {
            console.log('Done:', sum);
        }
    }
    
    chunk();
}
```

**Solução 2: Web Workers**

```javascript
// main.js
const worker = new Worker('worker.js');
worker.postMessage({ max: 10000000000 });

worker.onmessage = (e) => {
    console.log('Result:', e.data);
};

// worker.js (outra thread!)
onmessage = (e) => {
    let sum = 0;
    for (let i = 0; i < e.data.max; i++) {
        sum += i;
    }
    postMessage(sum);
};
```

### 3. Ordem de Promises encadeadas

```javascript
Promise.resolve()
    .then(() => console.log('1'))
    .then(() => console.log('2'));

Promise.resolve()
    .then(() => console.log('3'))
    .then(() => console.log('4'));

// Output: 1, 3, 2, 4
```

**Por quê?**

```
Microtask Queue inicial:
[() => console.log('1'), () => console.log('3')]

Executa '1', adiciona próximo .then:
[() => console.log('3'), () => console.log('2')]

Executa '3', adiciona próximo .then:
[() => console.log('2'), () => console.log('4')]

Executa '2':
[() => console.log('4')]

Executa '4':
[]
```

---

## Event Loop no Node.js

Node.js tem um Event Loop mais complexo com **fases**:

```
   ┌───────────────────────────┐
┌─>│           timers          │
│  │  (setTimeout, setInterval) │
│  └─────────────┬─────────────┘
│  ┌─────────────▼─────────────┐
│  │     pending callbacks     │
│  │    (I/O callbacks)        │
│  └─────────────┬─────────────┘
│  ┌─────────────▼─────────────┐
│  │       idle, prepare       │
│  │      (uso interno)        │
│  └─────────────┬─────────────┘
│  ┌─────────────▼─────────────┐
│  │           poll            │
│  │   (novos I/O events)      │
│  └─────────────┬─────────────┘
│  ┌─────────────▼─────────────┐
│  │           check           │
│  │     (setImmediate)        │
│  └─────────────┬─────────────┘
│  ┌─────────────▼─────────────┐
└──┤      close callbacks      │
   │  (socket.on('close'))     │
   └───────────────────────────┘
```

### process.nextTick

**Especial no Node.js**: executa **antes** de qualquer fase do Event Loop!

```javascript
console.log('1');

setImmediate(() => console.log('2'));

Promise.resolve().then(() => console.log('3'));

process.nextTick(() => console.log('4'));

console.log('5');

// Output: 1, 5, 4, 3, 2
```

**Ordem de prioridade no Node.js:**

1. Código síncrono
2. `process.nextTick` (nextTick Queue)
3. Promises (Microtask Queue)
4. Fases do Event Loop (timers, poll, check, etc.)

---

## Visualização Interativa

Para entender melhor, recomendo:

1. **Loupe**: http://latentflip.com/loupe/
   - Visualiza Call Stack, Web APIs, e Callback Queue em tempo real

2. **JSV9000**: https://www.jsv9000.app/
   - Visualiza Event Loop com microtasks e macrotasks

---

## Resumo

### Como JavaScript consegue ser concorrente com 1 thread?

1. **Call Stack** executa código JavaScript
2. **Web APIs** fazem trabalho pesado (I/O, timers) **fora da thread**
3. Quando concluem, callbacks vão para **queues**
4. **Event Loop** move callbacks das queues para stack quando ela está vazia

### Regras de Ouro

✅ **Código síncrono** sempre executa primeiro (na Call Stack)
✅ **Microtasks** (Promises) têm prioridade sobre **Macrotasks** (setTimeout)
✅ Event Loop **só pega da queue quando stack está vazia**
✅ **Nunca bloqueie** a Call Stack com código pesado

### Mental Model

```
JavaScript = 1 garçom muito eficiente
Event Loop = o sistema que organiza as tarefas
Web APIs = a cozinha (trabalha em paralelo)
Callbacks = avisos "pedido pronto!"

Garçom nunca para, nunca espera, sempre fazendo algo útil!
```

O Event Loop é o **coração** do JavaScript moderno - é o que permite Node.js servir milhares de conexões simultâneas e navegadores manterem interfaces responsivas!
