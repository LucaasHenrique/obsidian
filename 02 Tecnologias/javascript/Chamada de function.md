***
**Criado em**: 2025-04-02  
**Modificado em**: 18:54
**Topico**: #
***
#### Chamada com operador new

Quando uma função é chamada com o operador new, ela se comporta como um construtor, criando uma nova instância de um objeto. Neste caso, **this** refere-se à nova instância, e a função geralmente é usada para inicializar propriedades ou métodos da instância. Veja um exemplo no quadro abaixo:

```javascript
function Carro(marca) {
    this.marca = marca;
}

const meuCarro = new Carro("Toyota");
```
  
#### Chamada com funções de retorno (callbacks)

Em JavaScript, é comum usar funções como argumentos para outras funções, criando um mecanismo de "**callback**". Ao chamar uma função com um callback, o código pode ser assíncrono ou executar lógica adicional antes ou depois do callback. Veja um exemplo no quadro abaixo:

```javascript
function executarComCallback(callback) {
    console.log("Antes do callback");
    callback(); // Chama a função de retorno
    console.log("Depois do callback");
}

executarComCallback(() => {
    console.log("Callback executado");
});
```

