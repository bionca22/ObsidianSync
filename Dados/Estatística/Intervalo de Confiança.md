![[Pasted image 20241116173838.png]]
É o uso de dados amostrais para construir um intervalo, onde, o parâmetro da população vai estar com um certo grau de confiança.
Quanto maior o intervalo maior a chance da média populacional cair dentro desse intervalo, por exemplo.

---
##### Intervalo de Confiança para a Média

Como dito no [[Teorema do Limite Central]], uma amostra grande o suficiente terá uma média com com distribuição normal.
Então uma possibilidade que temos é fazer um intervalo com x% de confiança usando a média da amostra que temos e assumir que nossa média amostral estará dentro desse intervalo.

>[!tip] Quanto maior o nível / porcentagem dessa confiança, maior será o intervalo 

- **Exemplo prático**: Imagine que você mediu a altura média de um grupo de pessoas e obteve **1,75 m** como média amostral. Você calcula um IC de 95% para essa média, que resulta no intervalo de 1,70 m a 1,80 m. Isso significa que **há 95% de confiança de que a média verdadeira da população esteja dentro dessa faixa.**
    
- **Interpretação**: Um IC de 95% **não** significa que há 95% de probabilidade de a média populacional estar no intervalo calculado (porque a média populacional é fixa, mesmo que desconhecida). O que significa é que, **se você repetisse o estudo várias vezes**, 95% dos ICs construídos a partir de novas amostras conteriam a verdadeira média populacional.

#### Fatores que afetam o intervalo de confiança

1. **Tamanho da amostra (n)**:
    
    - Amostras maiores fornecem estimativas mais precisas da média, porque a variabilidade nos dados tende a diminuir com mais observações.
    - **Efeito prático**:
        - Amostras maiores levam a **intervalos de confiança mais estreitos** (menor margem de erro).
        - Exemplo: Com 10 observações, seu IC pode ser 1,70 m a 1,80. Com 100 observações, pode ser 1,74 m a 1,76 m.

1. **Variabilidade nos dados (s)**:
    
    - Variabilidade é uma medida de quão espalhados os dados estão (desvio padrão da amostra, s).
    - **Efeito prático**:
        - Amostras com maior variabilidade resultam em **intervalos de confiança mais largos**, porque há mais incerteza sobre a média.
        - Exemplo: Se a altura dos indivíduos na amostra varia entre 1,50m 2,00m, o IC será mais largo do que se as alturas estiverem concentradas entre 1,70 m 1,80m.

----

### Intervalo de Confiança para Proporção

Proporção = é basicamente a razão da parte pelo todo, uma representação do todo.

![[Pasted image 20241117101304.png]]

##### **2. Intervalo de Confiança para Proporção:**

É uma variação do intervalo de confiança geral, usado especificamente para **variáveis categóricas**, quando queremos estimar uma proporção populacional (p), como a proporção de pessoas que votam em um candidato, ou de produtos defeituosos em uma linha de produção.

- **Parâmetro alvo:** A proporção populacional (p).
- **Cálculo:** Baseia-se na proporção amostral (+​) como ponto central, com a fórmula:
![[Pasted image 20241117102735.png]]
Esse intervalo é usado quando estamos trabalhando com **dados categóricos** (sim/não, sucesso/falha, etc.).

![[Pasted image 20241117103035.png]]