***
**Criado em**: 2025-08-01  
**Modificado em**: 21:22
**Topico**: #
***
> em cada etapa, a busca verifica o elemento do meio da região ativa. Se
   o elemento do meio for o elemento alvo, a busca termina. Caso contrário, a busca continua recursivamente para a metade esquerda ou direita da região, dependendo do valor do elemento do meio

metodo 2: 

>busca percorre o array da esquerda para a direita, e o comprimento inicial do salto é n/2. Em cada etapa, o comprimento do salto será dividido pela metade: primeiro n/4, depois n/8, n/16, etc., até que finalmente o comprimento seja 1. Após os saltos, ou o elemento alvo foi encontrado ou sabemos que ele não aparece no array.

```c++
int k = 0;
for (int b = n/2; b >= 1; b /= 2) {
	while (k+b < n && array[k+b] <= x) k += b;
}
if (array[k] == x) {
	return k;
}
```

funções baseadas em busca binaria: 
• lower_bound retorna um ponteiro para o primeiro elemento do array cujo
valor é pelo menos x.
• upper_bound retorna um ponteiro para o primeiro elemento do array cujo
valor é maior do que x.
• equal_range retorna ambos os ponteiros acima.
***
# Busca binária nas respostas

problemas que envolvem minimizar ou maximizar algo podem ser formulados de uma maneira q seja possivel resolver com binary search;

# Ex: Restaurente quer o numero minimo  de garçons necessario para atender todo mundo.

Se soubessemos que o numero minimo necessario é 5, o que podemos concluir sobre os outros?

qualquer N menor q 5 não serve. 

ao inves de de tentar achar na força bruta, podemos tentar chutar um N e utilizar bin search para saber se esse numero está mais a esquerda ou direita. Vale se a sequencia for ordenada. Fazemo O(NlogN) comparações;
***
