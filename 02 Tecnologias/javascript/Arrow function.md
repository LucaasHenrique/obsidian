***
**Criado em**: 2025-04-02  
**Modificado em**: 18:21
**Topico**: #
***
O corpo das arrow functions pode ser uma expressão ou um bloco de código. Se for uma expressão, o retorno é implícito, o que significa que não é necessário usar a palavra-chave return. 

```javascript
const quadrado = x => x * x;
```

```javascript
const calcular = (a, b) => {
  const resultado = a + b;
  return resultado;
};
```


##### Contexto this

>Escopo léxico é uma maneira de definir como variáveis e funções são acessadas com base na posição em que foram definidas no código-fonte. Em JavaScript, uma função tem acesso ao seu próprio escopo, ao escopo de qualquer função que a envolva e ao escopo global.   

>O **this** é uma palavra-chave que refere-se ao contexto no qual uma função está sendo executada. Nas funções tradicionais, o contexto this é dinâmico, significando que ele pode mudar dependendo de como a função é chamada. Isso pode gerar confusão, especialmente em callbacks ou métodos que são usados em contextos variados. As arrow functions, por outro lado, têm um comportamento diferente: elas não têm seu próprio **this**, mas usam o contexto léxico do local onde foram definidas.

##### Arrow functions e closures
As arrow functions, como outras funções em JavaScript, podem criar closures. Um closure ocorre quando uma função "lembra" das variáveis e do contexto do escopo onde foi definida, mesmo quando é usada fora desse escopo.