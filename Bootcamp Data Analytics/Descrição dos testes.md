### ANOVA
 é usada para variáveis dependentes contínuas e independentes categóricas com três ou mais níveis.
 
 ## **Como calcular teste ANOVA?**
O cálculo para o teste ANOVA envolve várias etapas, e pode parecer complexo, especialmente se você estiver fazendo à mão. Entretanto, geralmente, é realizado utilizando um software de estatística. Aqui está um resumo das etapas:

- **Calcular a média de cada grupo**: Para cada grupo de dados, calcule a média;
- **Calcular a soma dos quadrados dentro dos grupos (SSW)**: Para cada grupo, subtraia a média do grupo de cada valor individual para obter a diferença, eleve ao quadrado cada diferença e, em seguida, some todos esses valores quadrados. A soma desses valores para todos os grupos é a SSW;
- **Calcular a soma total dos quadrados (SST)**: Subtraia a média geral (a média de todos os valores, independentemente do grupo) de cada valor individual, eleve ao quadrado cada diferença, e então some todos esses valores quadrados;
- **Calcular a soma dos quadrados entre os grupos (SSB)**: Isso é igual à SST menos a SSW;
- **Calcular os graus de liberdade**: O número de graus de liberdade para SSW é o número total de observações menos o número de grupos. O número de graus de liberdade para SSB é o número de grupos menos 1;
- **Calcular as variâncias médias**: A variância média dentro dos grupos (MSW) é a SSW dividida pelos graus de liberdade associados à SSW. A variância média entre os grupos (MSB) é a SSB dividida pelos graus de liberdade associados à SSB;
- **Calcular a estatística F**: A estatística F é a MSB dividida pela MSW;
- **Obter o valor de p**: Use a distribuição F com os graus de liberdade apropriados para obter o valor de p correspondente à estatística F. Se o valor de p for menor que o nível de significância escolhido (geralmente 0.05), você rejeita a hipótese nula de que todas as médias do grupo são iguais.

https://www.fm2s.com.br/blog/anova
----
