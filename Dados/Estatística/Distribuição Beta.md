A distribuição beta é uma distribuição de probabilidade contínua definida no intervalo [0,1], frequentemente usada para modelar incertezas sobre probabilidades. Ela é parametrizada por dois parâmetros positivos, α\alphaα (alfa) e β\betaβ (beta), que determinam a forma da distribuição. A função densidade de probabilidade (PDF) da distribuição beta é dada por:

![[Pasted image 20250106102001.png]]

### Principais características:

1. **Intervalo:** A distribuição beta é restrita ao intervalo [0,1], tornando-a ideal para modelar variáveis que representam proporções ou probabilidades.
    
2. **Parâmetros:**
    - α: Controla o "peso" da distribuição na direção de valores mais próximos de 1.
    - β: Controla o "peso" da distribuição na direção de valores mais próximos de 0.
    - Quando α>1e β>1, a distribuição é unimodal, com uma "barriga" mais alta no intervalo.
    - Quando α<1ou β<1, a distribuição se torna mais inclinada para um dos extremos.
3. **Média e Variância**
	- ![[Pasted image 20250106104857.png]]
4. **Flexibilidade:** Com os parâmetros α e β, a distribuição beta pode assumir várias formas:
	- Simétrica (α=β).
	- Assimétrica, com picos em 0 ou 1 dependendo de α e β.


### Aplicações:

A distribuição beta é amplamente usada em várias áreas, como:

- **Modelagem bayesiana:** Usada como distribuição a priori para probabilidades.
- **Análise de proporções:** Para modelar incertezas em proporções observadas.
- **Gerenciamento de projetos:** No método PERT, para estimar tempos de conclusão.