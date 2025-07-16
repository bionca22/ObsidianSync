

A distribuição normal é uma das distribuições de probabilidade mais importantes e amplamente utilizadas em estatística e probabilidade. Ela é também conhecida como distribuição gaussiana (em homenagem a Carl Friedrich Gauss, que fez importantes contribuições para essa área).

![[Pasted image 20241111173940.png]]

A distribuição normal é uma distribuição contínua, ou seja, é usada para descrever variáveis que podem assumir um número infinito de valores dentro de um intervalo contínuo. Ela é caracterizada por uma forma de sino simétrica, com a maior parte dos dados concentrados em torno da média e distribuídos de forma gradual para os dois lados.

![[Pasted image 20241111182735.png]]

Essa fórmula descreve a probabilidade de uma variável aleatória xxx assumir um determinado valor, dado que ela segue uma distribuição normal.

### Características Principais da Distribuição Normal

- **Simetria**: A distribuição normal é perfeitamente simétrica em torno de sua média (μ\muμ). Isso significa que a probabilidade de um valor estar à esquerda da média é igual à probabilidade de estar à direita.
    
- **Forma de Sino**: A curva da distribuição tem a forma de um sino. A maior parte dos valores se concentra perto da média, e a probabilidade diminui à medida que você se afasta da média.
    
- **Média, Mediana e Moda**: Na distribuição normal, a média, a mediana e a moda são iguais e localizadas no centro da curva.
    
- **Desvio Padrão e a Regra Empírica**: O desvio padrão (σ\sigmaσ) controla a "largura" da curva. Quanto maior o desvio padrão, mais espalhada a curva será.
    
    A "Regra Empírica" (ou regra dos 68-95-99,7) descreve a distribuição de dados em torno da média:
    
    - Aproximadamente **68%** dos valores estão dentro de 1 desvio padrão da média.
    - Aproximadamente **95%** dos valores estão dentro de 2 desvios padrões da média.
    - Aproximadamente **99,7%** dos valores estão dentro de 3 desvios padrões da média.

#### A Distribuição Normal Padrão

A **distribuição normal padrão** é um caso específico da distribuição normal onde a média é 000 e o desvio padrão é 111. Ela é denotada por N(0,1)N(0, 1)N(0,1).

Para trabalhar com distribuições normais que não sejam padrão, você pode usar a **padronização**. A padronização transforma qualquer distribuição normal para a distribuição normal padrão. Isso é feito através da fórmula:
![[Pasted image 20241111184627.png]]

A transformação Z é útil porque a tabela da distribuição normal padrão (ou tabela Z) nos fornece as probabilidades associadas aos valores padronizados.

#### Propriedades Importantes

- **Áreas sob a curva**: A área sob a curva da distribuição normal entre dois valores x1x_1x1​ e x2x_2x2​ representa a probabilidade de que uma variável aleatória XXX assumirá um valor entre x1x_1x1​ e x2x_2x2​. Como a soma de todas as probabilidades para uma distribuição normal é 1, a área total sob a curva é igual a 1.
    
- **Simetria e Probabilidades**: Como a distribuição normal é simétrica em torno de sua média, se você quiser calcular a probabilidade de que XXX seja maior do que a média, a probabilidade será 0,5 (ou 50%). O mesmo vale para valores menores que a média.

#### Usos na Estatística

- **Inferência estatística**: Muitas técnicas de amostragem, como o teste de hipóteses e intervalos de confiança, assumem que os dados seguem uma distribuição normal.
- **Modelagem de erros e fenômenos naturais**: A distribuição normal é frequentemente usada para modelar fenômenos como alturas de pessoas, erros de medição, e outros fenômenos naturais que seguem esse padrão.

![[Pasted image 20241111191550.png]]
100 lançamentos de 200 moedas não é o suficiente para  ver a curva de uma distribuição normal.
É necessário obter mais dados de experimento.
![[Pasted image 20241111191623.png]]


### Distribuição Normal  - Área 
_____

![[Pasted image 20241112185031.png]]

____

Na distribuição normal, a área sob a curva representa a probabilidade acumulada de um valor aleatório cair entre certos limites. No caso específico da média e dos desvios-padrão na distribuição normal padrão (ou seja, uma distribuição normal com média μ=0\mu = 0μ=0 e desvio-padrão σ=1\sigma = 1σ=1), podemos entender a área entre a média e um desvio-padrão acima dela (isto é, até z=1z = 1z=1).

Para isso, considere os seguintes pontos:

1. **Propriedade da simetria**: A curva da distribuição normal é simétrica em relação à média. Portanto, a probabilidade de um valor estar acima ou abaixo da média é de 50%.

> [!Explicação]
> A simetria na distribuição normal acontece devido à forma como essa distribuição é definida matematicamente.
> 
> **Propriedade da Simetria**: Na prática, essa simetria significa que a curva da distribuição normal tem a mesma forma à esquerda e à direita da média. Como resultado, qualquer ponto à esquerda da média (como μ−1σ\mu - 1\sigmaμ−1σ) terá uma "imagem espelhada" à mesma distância para a direita (como μ+1σ\mu + 1\sigmaμ+1σ). A área (ou probabilidade) associada a um intervalo na curva é a mesma dos dois lados da média.
> 
> **Probabilidade de 50%**: Como a curva é simétrica e a média é o ponto central dessa simetria, a área total (que representa a probabilidade total de 100%) divide-se igualmente entre os dois lados da média:

- A área à esquerda da média representa 50% da probabilidade total.
- A área à direita da média também representa 50% da probabilidade total.

2. **Regra empírica dos 68-95-99,7%**: Essa regra indica aproximadamente quanto da área total da curva está dentro de 1, 2 e 3 desvios-padrão da média:

- Cerca de **68% dos valores** estão dentro de −1 e +1 desvios-padrão da média.
- Cerca de **95%** estão entre −2- e +2 desvios-padrão.
- Cerca de **99,7%** estão entre −3 e +3 desvios-padrão.

> [!note] Explicação 
> 
> A **Regra Empírica dos 68-95-99,7%**, também conhecida como **Regra dos Três Sigmas**, descreve a distribuição dos dados em torno da média em uma **distribuição normal**. Ela estima a proporção de dados dentro de múltiplos desvios-padrão da média.
> 
>  **1. 68% dos dados dentro de 1 desvio-padrão**
>  Na distribuição normal:
>  - **34% dos dados** estão entre a média e +1 desvio-padrão (μ até μ+σ).
>  -  **34% dos dados** estão entre a média e −1 desvio-padrão (μ até μ−σ).
>Somando esses dois lados (à esquerda e à direita da média), temos que cerca de **68% dos dados** estão entre μ−σ e μ+σ.
>
>e assim por diante.

----
#### Quando a Normalização é Necessária?


Em muitos casos, a normalização dos dados é necessária para que diferentes variáveis tenham escalas comparáveis, evitando que uma variável domine o modelo simplesmente por ter valores maiores.

**Normalização** é um processo que visa colocar as variáveis em uma escala comum, geralmente entre 0 e 1 ou com média 0 e desvio padrão 1.

**Benefícios da normalização:**

- Evita que variáveis com maior magnitude dominem o modelo.
- Permite a comparação justa entre variáveis em diferentes escalas.
- Melhora a performance de muitos algoritmos de aprendizado de máquina.

**Quando normalizar:**

- **Escalas muito diferentes:** Variáveis com grande diferença de magnitude.
- **Unidades diferentes:** Variáveis medidas em unidades distintas.
- **Algoritmos sensíveis à escala:** Alguns algoritmos, como K-means e redes neurais, são mais sensíveis à escala dos dados.

**Métodos comuns de normalização:**

- **Min-max:** Escala os dados para um intervalo específico, geralmente entre 0 e 1. É útil quando os dados têm muitos outliers, pois reduz o impacto deles ao centrar os dados em torno da mediana.
	![[Pasted image 20241113163146.png]]

- **Z-score:** Padroniza os dados, resultando em uma média de 0 e desvio padrão de 1.É útil quando você quer preservar a distribuição dos dados, mas trazê-los para uma escala comparável.
	![[Pasted image 20241113163028.png]]

- **Escalonamento robusto**: Usa a mediana e o intervalo interquartil (IQR) em vez da média e do desvio padrão, o que pode ser útil em dados com muitos outliers.
	![[Pasted image 20241113163251.png]]
----
#### Importante Lembrar

**distribuição uniforme**: A probabilidade de uma observação ocorrer é a mesma para todos os dados

**distribuição simétrica**:  A média, moda e mediana são iguais. 
Em distribuições simétricas, o valor central (ou ponto de simetria) coincide com a média (valor esperado), a mediana (ponto que divide a distribuição ao meio) e a moda (valor com maior frequência, se houver uma única moda). Isso ocorre, por exemplo, na distribuição normal e em outras distribuições simétricas.


> [!tip] desvio padrão é uma medida de dispersão, enquanto a média é uma medida de centralidade.

> [!tip] Se uma distribuição tiver mais de uma moda, ela será chamada de **distribuição multimodal**, o que pode ou não ser simétrico. Por exemplo, uma distribuição bimodal com dois picos de mesma altura pode ser simétrica, mas isso não é uma regra geral para distribuições simétricas.

