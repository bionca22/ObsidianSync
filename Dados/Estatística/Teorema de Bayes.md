![[Pasted image 20241207095341.png]]

![[Pasted image 20241207095645.png]]

Exemplo:
- probabilidade de ter câncer = 1% probabilidade de uma pessoa com câncer ter o exame positivo = 99% - probabilidade de uma ´pessoa que não tem câncer ter o exame negativo = 99.5%

### Variáveis utilizadas

1. **A**: A pessoa tem câncer.
    - Probabilidade: P(A)=0,01 (1%).
2. **¬A**: A pessoa **não** tem câncer.
    - Probabilidade: P(¬A)=0,99 (99%).
3. **B**: O teste deu positivo.
    - O que queremos calcular: P(A∣B), a probabilidade de ter câncer dado um teste positivo.
4. **¬B**: O teste deu negativo.

![[Pasted image 20241207102429.png]]

![[Pasted image 20241207102733.png]]
### Interpretação do resultado

Se o teste deu positivo, a probabilidade de a pessoa ter câncer (mesmo sendo inicialmente rara, 1%) sobe significativamente para **66,7%**, devido à alta sensibilidade e especificidade do teste. Isso demonstra como o teste atualiza a probabilidade inicial (P(A)P(A)P(A)) considerando a evidência fornecida pelo resultado positivo (BBB).




## Exemplo 2

Considere que a probabilidade de uma pessoa viajar é de 10%, a probabilidade dela estar de férias é de 20% e a probabilidade dela viajar durante as férias é de 5%. Qual a probabilidade dessa pessoa estar de férias ou viajar?


# Probabilidade de Estar de Férias ou Viajar

## Dados do Problema
- $A$: A pessoa vai viajar.  
  $P(A) = 0,1$ (10%).  
- $B$: A pessoa está de férias.  
  $P(B) = 0,2$ (20%).  
- A pessoa vai viajar **durante as férias**:  
  $P(A \cap B) = 0,05$ (5%).


## Fórmula Utilizada
A probabilidade de a pessoa estar de férias **ou** viajar é dada por:

$$
P(A \cup B) = P(A) + P(B) - P(A \cap B)
$$

## Cálculo
Substituímos os valores conhecidos:

$$
P(A \cup B) = 0,1 + 0,2 - 0,05
$$

$$
P(A \cup B) = 0,25 \, (25\%)
$$

## Conclusão
A probabilidade de a pessoa **estar de férias ou viajar** é **25%**.  
Isso leva em conta que os dois eventos podem ocorrer simultaneamente (viajar durante as férias), e essa sobreposição foi subtraída para evitar contagem dupla.

---

As demais afirmações estão corretas:

- A Estatística Bayesiana realmente trata a probabilidade como uma medida de crença.
- A probabilidade a priori é uma probabilidade inicial, antes de incorporar novas evidências.
- A probabilidade a posteriori é calculada com base em informações novas.
- A probabilidade condicional atualiza as crenças com base em evidências observadas.

---
## Redes Bayesianas

![[Pasted image 20250104102752.png]]

![[Pasted image 20250104102927.png]]

