
#### O que é o Teorema do Limite Central?

O Teorema do Limite Central afirma que, **dada uma amostra aleatória suficientemente grande de uma população com qualquer distribuição**, a média da amostra (ou a soma) tende a se aproximar de uma distribuição normal. Isso acontece mesmo se a distribuição original dos dados não for normal.

Mais formalmente:

- Se você tirar várias amostras independentes de uma população qualquer (não necessariamente normal) e calcular a média dessas amostras, à medida que o tamanho da amostra aumenta, a distribuição dessas médias amostrais tende a uma distribuição normal.
- Este comportamento acontece com tamanhos de amostras suficientemente grandes (geralmente acima de 30 é considerado suficiente, mas isso pode variar dependendo da distribuição inicial).

#### Intuição por Trás do Teorema

O TLC é poderoso porque permite que estatísticos e cientistas façam inferências sobre uma população mesmo que a distribuição dos dados seja desconhecida ou não-normal. Ao dizer que a média das amostras se aproxima de uma distribuição normal, o teorema permite que cálculos como intervalos de confiança e testes de hipótese sejam aplicados com métodos baseados na normalidade.

Para entender melhor, imagine que você esteja tentando analisar uma variável que tem uma distribuição altamente assimétrica, como o tempo de espera em uma fila, o qual geralmente tem muitos valores pequenos e alguns valores muito altos. Mesmo que a distribuição dos tempos de espera seja irregular, as médias das amostras desses tempos de espera tendem a seguir uma distribuição normal.

> [!note] Explicação 
> ### Exemplo de Tempos de Espera em uma Fila
> 
Suponha que estamos observando os tempos de espera (em minutos) em uma fila. Os tempos de espera são irregulares e têm uma distribuição assimétrica. Aqui estão os tempos de espera para 15 pessoas, o que representa a "população":

- **Tempos de Espera**: 1, 2, 2, 3, 3, 4, 5, 6, 6, 7, 8, 10, 15, 20, 25

A média populacional desses tempos é de aproximadamente **7,4 minutos**, mas a distribuição é claramente assimétrica com uma longa cauda à direita.

### Passo 1: Tirando Amostras Pequenas

Vamos tirar várias amostras aleatórias de tamanho 5 (isto é, cinco tempos de espera de cada vez) dessa população e calcular a média de cada amostra.

Aqui estão algumas amostras e suas médias (escolhidas aleatoriamente):

1. Amostra: [1, 2, 3, 5, 6] → Média = (1 + 2 + 3 + 5 + 6) / 5 = **3,4**
2. Amostra: [3, 4, 6, 7, 8] → Média = (3 + 4 + 6 + 7 + 8) / 5 = **5,6**
3. Amostra: [2, 6, 10, 15, 20] → Média = (2 + 6 + 10 + 15 + 20) / 5 = **10,6**
4. Amostra: [3, 3, 5, 7, 25] → Média = (3 + 3 + 5 + 7 + 25) / 5 = **8,6**
5. Amostra: [1, 2, 4, 6, 10] → Média = (1 + 2 + 4 + 6 + 10) / 5 = **4,6**

Cada média calculada acima é a **média de uma amostra** de tamanho 5.

### Passo 2: Distribuição das Médias das Amostras

Agora, vamos ver as médias de várias amostras:

- Médias das amostras: 3,4; 5,6; 10,6; 8,6; 4,6...

Se continuássemos esse processo várias vezes (com dezenas ou centenas de amostras), teríamos uma coleção de médias amostrais.

### Observando o Comportamento da Distribuição das Médias

Vamos considerar um exemplo com 10 médias amostrais, para ilustrar o conceito. Suponha que tiramos mais algumas médias e temos a seguinte lista de médias amostrais:

- Médias amostrais: **3,4; 5,6; 10,6; 8,6; 4,6; 7,0; 6,2; 7,4; 8,2; 5,8**

Ao traçar a distribuição desses valores médios, perceberemos que ela se aproxima de uma forma mais simétrica do que a distribuição original dos tempos de espera individuais, mesmo com uma quantidade limitada de amostras.

Se aumentarmos o tamanho das amostras de 5 para, digamos, 30 (se tivéssemos uma população maior), a média de cada amostra começaria a variar ainda menos em relação à média populacional de 7,4. À medida que aumentamos o tamanho da amostra, a distribuição das médias amostrais se aproxima cada vez mais de uma distribuição normal com média próxima à média populacional, **independentemente da forma da distribuição original** dos tempos de espera individuais.

![[Pasted image 20241113165606.png]]
