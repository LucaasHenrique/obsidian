***
**Criado em**: 2025-05-02  
**Modificado em**: 14:59
**Topico**: #
***
Middlewares no Node.js (especialmente com o framework Express) são funções intermediárias que têm acesso ao objeto de requisição (req), ao objeto de resposta (res) e à função next(), que indica quando o middleware terminou e o próximo deve ser chamado.

Eles são usados para interceptar e processar requisições antes de chegarem ao endpoint final. Podem servir para várias finalidades, como:

    Autenticação/autorização

    Log de requisições

    Validação de dados

    Tratamento de erros

    Manipulação de cabeçalhos ou cookies

Estrutura básica de um middleware:

```javascript
function meuMiddleware(req, res, next) {
  console.log('Middleware executado');
  next(); // chama o próximo middleware ou rota
}
```


Exemplo com Express:


``` javascript 
const express = require('express');
const app = express();

// Middleware global
app.use((req, res, next) => {
  console.log(`${req.method} ${req.url}`);
  next();
});

// Rota
app.get('/', (req, res) => {
  res.send('Olá, mundo!');
});

app.listen(3000, () => console.log('Servidor rodando'));
```


Você pode encadear quantos middlewares quiser, e eles são executados na ordem em que foram definidos.