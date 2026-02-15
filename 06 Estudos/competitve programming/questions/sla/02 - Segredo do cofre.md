***
**Criado em**: 2025-09-24  
**Modificado em**: 21:12
**Topico**: #
***
basicamente um barra de n elementos numerados de 0-9, o usuario pode deslizar um controle tanto para como esquerda: 

"O segredo vai depender de quantas vezes cada um dos dez inteiros entre 0 e 9 vai aparecer dentro do controle. Por exemplo, suponha que o dono deslize o controle da posição inicial 1 até a posição 9, depois para a posição 4, depois para a posição 11 e por fim até a posição 13. Veja que o inteiro 1, por exemplo, vai aparecer seis vezes dentro do controle; e o inteiro 9 vai aparecer quatro vezes."

A primeira linha da entrada contém dois inteiros N e M, representando o número de posições na barra do cofre e o número de posições na sequência que o dono vai seguir para deslizar o controle. A segunda linha contém N inteiros entre 0 e 9, definindo a barra do cofre. A terceira linha contém M inteiros representando a sequência de posições que o dono vai seguir. A primeira posição nessa sequência é sempre 1 e não há duas posições consecutivas iguais.
***

cada deslize de controle pode ser visto com uma operação num intervalo [l, r] de adicionar um determinado valor **D** à frequência de cada elemento neste intervalo.
