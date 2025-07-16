

![[Pasted image 20250108194334.png]]
O modelo de Markov consiste basicamente em um sistema que não considera o evento passado ao tentar definir a probabilidade de um evento futuro acontecer. 

###### Exemplo 
Imagine que uma cantina serve apenas 3 tipos de comida. Para iniciar o modelo teríamos de observar por algum tempo a probabilidade com que as comidas são servidas uma após a outra.

![[Pasted image 20250108194845.png]]

Digamos que em um dia foi servido pizza e no dia seguinte foi servido hambúrguer, a probabilidade de servir pizza mais uma vez no terceiro dia é de 0.6 contra 0.2 de servir hambúrguer novamente e 0.2 de servir cachorro quente, independentemente de já se ter servido pizza antes ou hambúrguer ainda mais recentemente. Esse é um conceito importante chamado Propriedade de Markov. 

Outra propriedade importante é a de que a soma das probabilidades de mudança de estado tem de ser igual a 1 por estarmos tratando de probabilidade. Se der um número menor significa que alguma probabilidade está faltando.