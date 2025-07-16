![[Pasted image 20241117141701.png]]

**Hipótese Nula H0**: 
- Representa o estado atual ou uma suposição inicial.
- É geralmente uma declaração de "ausência de efeito" ou "sem diferença".

**Hipótese Alternativa H1**: 
- É uma afirmação a respeito do parâmetro que aceitamos como provavelmente verdadeiro caso H0 seja rejeitado.
-  Representa o estado atual ou uma suposição inicial.
- É geralmente uma declaração de "ausência de efeito" ou "sem diferença".

**Nível de Significância (α):**
- Probabilidade máxima de cometer um **Erro Tipo I** (rejeitar H0​ quando ela é verdadeira).
- Valores comuns: 0,05 (5%) ou 0,01 (1%).

**Estatística de Teste:**
- Uma métrica calculada a partir dos dados amostrais, usada para decidir entre H0 e H1​.
- Exemplo: teste z, teste t, teste qui-quadrado, etc.

**Valor p:**
- Probabilidade de obter um resultado tão extremo (ou mais) quanto o observado, assumindo que H0​ é verdadeira.
- Se p≤α, rejeitamos H0​.
- quanto menor  o P valor, mais evidência há para se rejeitar a hipótese nula 

![[Pasted image 20241117142324.png]]

#### **Passos para Realizar um Teste de Hipóteses**

1. **Definir as Hipóteses:**
    
    - Estabeleça H0​ e H1​ com base no problema.

1. **Escolher o Teste Estatístico:**
    
    - Depende do tipo de dados e do objetivo:
        - z-teste para médias com variância conhecida e amostras grandes.
        - t-teste para médias com variância desconhecida e amostras pequenas.
        - Qui-quadrado para variáveis categóricas.
        
1. **Calcular a Estatística de Teste:**
    
    - Usar os dados amostrais para calcular o valor do teste.

1. **Definir a Regra de Decisão:**
    
    - Baseado no nível de significância (α), determine a região crítica (onde rejeitamos H0).

1. **Tomar a Decisão:**
    
    - Compare a estatística de teste com o valor crítico, ou analise o valor p.
    - Se p≤α, **rejeite H0​**.


![[Pasted image 20241117144230.png]]


![[Pasted image 20241118141327.png]]

![[Pasted image 20241118141354.png]]


https://www.youtube.com/watch?v=h4QcWDDlrW0&list=PL7xT0Gz6G0-TfV-S6WiGDvIsZds6Pv_g8&index=1&pp=iAQB

#### Outros Tipos de Testes

**Teste Anderson Darling**: é usado para testar se uma amostra de dados veio de uma população com  uma distribuição específica.

**Kruskal wallis**: testa a hipótese nula de que a população mediana de todos os grupos são iguais. Este é um teste não paramétrico, ou seja, não depende de nenhum parâmetro da população como, por exemplo, a média.

**kolmogorov-Smirnov:** ou testeKS responde à pergunta "Qual a probabilidade de que essas amostra possa ter sido extraída dessa distribuição?" "esses dois dados foram extraidos da mesma distribuição? (desconhecida)"

![[Teste de hipótese.pdf]]