
##### **Distribuição discreta vs. distribuição contínua**

1. **Distribuição discreta**:
    
    - Trata de variáveis aleatórias que podem assumir apenas valores específicos e isolados.
    - Exemplo: X=0,1,2,3,…X = 0, 1, 2, 3, \dotsX=0,1,2,3,… (valores inteiros não negativos).
    - A probabilidade é calculada diretamente para cada valor específico, P(X=k)P(X = k)P(X=k).
    
2. **Distribuição contínua**:
    
    - Lida com variáveis aleatórias que podem assumir **qualquer valor dentro de um intervalo contínuo**.
    - Exemplo: X pode ser qualquer valor real entre a e b, como 1,37 ou 4,58.
    - A probabilidade de assumir um valor exato (P(X=x)) é zero; usamos densidade de probabilidade (f(x)) para calcular probabilidades em intervalos, como P(a≤X≤b).

>[!tip] o Teorema do Limite central vale para ambas as distribuições

---
### O intervalo [0,1]
O intervalo [0,1]  significa que a variável aleatória X descrita por essa distribuição só pode assumir valores dentro desse intervalo, ou seja, X ∈ [0,1].

 - No contexto de probabilidades, [0,1] é o intervalo natural, já que probabilidades nunca são menores que 0 nem maiores que 1.

**Interpretação prática:**
 Se você está modelando algo que sempre está entre 0 e 1, como a chance de sucesso em um teste, a fração de uma população que tem uma característica específica ou a fração do tempo de um processo concluído, a distribuição beta é uma escolha apropriada.
-  Se X=0.3, isso pode significar que 30% de uma amostra tem uma certa característica.
- Se X=0.8, pode significar uma probabilidade de 80% de sucesso em um evento.

----


#### Probabilidade Condicional 
![[Pasted image 20241119185002.png]]

A probabilidade condicional mede a chance de um evento ocorrer **dado que outro evento já ocorreu**. Ou seja, é uma maneira de atualizar nossas expectativas sobre a probabilidade de algo acontecer quando sabemos alguma informação extra.

A notação para a probabilidade condicional é:

![[Pasted image 20241119185514.png]]

##### Fórmula de Probabilidade Condicional

A fórmula é:

![[Pasted image 20241119185335.png]]

##### Exemplo Simples

Imagine um baralho de 52 cartas. Qual é a probabilidade de tirar uma carta de espadas (A), dado que você sabe que a carta retirada foi preta (B)?

![[Pasted image 20241119185429.png]]
Isso significa que, sabendo que a carta é preta, a probabilidade de ela ser de espadas é **50%**.

---

## Teorema das Probabilidades

### **1. Teorema da Adição**

Este teorema é usado para calcular a probabilidade de **união de eventos**, ou seja, a probabilidade de que **pelo menos um de dois eventos ocorra**.

Para dois eventos A e B, a fórmula é:

	P(A∪B)=P(A)+P(B)−P(A∩B)

- P(A∪B): probabilidade de A ou B ocorrer (união).
- P(A: probabilidade de A ocorrer.
- P(B): probabilidade de B ocorrer.
- P(A∩B): probabilidade de A e B ocorrerem ao mesmo tempo.

Se A e B são **mutuamente exclusivos** (não podem ocorrer ao mesmo tempo), então P(A∩B)=0, e a fórmula se simplifica para:

	P(A∪B)=P(A)+P(B)

---

### **2. Teorema da Multiplicação**

Este teorema é usado para calcular a probabilidade de dois eventos **ocorrerem juntos** (interseção).

Para dois eventos A e B, a fórmula é:

	P(A∩B)=P(A)⋅P(B|A)

- P(A∩B): probabilidade de A e B ocorrerem juntos.
- P(A): probabilidade de A ocorrer.
- P(B∣A): probabilidade de B ocorrer dado que A já ocorreu.

Se AAA e BBB são **independentes** (o resultado de um não afeta o outro), então P(B∣A)=P(B), e a fórmula se simplifica para:

	P(A∩B)=P(A)⋅P(B)

---

### **3. Teorema de Bayes**

Esse teorema é uma extensão do conceito de probabilidade condicional. Ele é usado para calcular P(A∣B) quando sabemos P(B∣A).

A fórmula é:

![[Pasted image 20241119190721.png]]

Esse teorema é amplamente usado em inferência estatística, diagnóstico médico e aprendizado de máquina.
