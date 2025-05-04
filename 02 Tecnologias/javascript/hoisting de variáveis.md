***
**Criado em**: 2025-04-02  
**Modificado em**: 09:13
**Topico**: #javascript 
***
 >Uma característica peculiar do JavaScript é que as variáveis podem ser usadas antes de serem declaradas, sem causar um erro. Esse comportamento é conhecido como "**elevação** " ou "**hoisting**". Ele ocorre porque, quando um script é carregado, o JavaScript move as declarações de variáveis para o início (topo) do escopo.
 
console.log(x); // undefined
var x = 10;
console.log(x); // 10