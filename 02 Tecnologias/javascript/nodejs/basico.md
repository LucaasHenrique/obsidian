***
**Criado em**: 2025-04-14  
**Modificado em**: 10:08
**Topico**: #
***
Exemplo basico: 

```javascript
import express from 'express';

const server = express();

// Query params = http://localhost:8080/?name=lucas$idade=19
// Route params = http://localhost:8080/hello/id

server.get('/hello', (req, res) => {
	const {nome, idade} = req.query;
	
	return res.json({
		tilte: "Hello Word",
		message: `Olá ${nome}, tudo bem com você?`,
		idade: idade
	});
});

server.get('/hello/:nome', (req, res) => {
	const nome = req.params.nome;
	
	return res.json({
		tilte: "Hello Word",
		message: `Olá ${nome}`,
	});
});

  

server.listen(8080);
```


