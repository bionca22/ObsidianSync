

Machine learning significa aprendizado de máquina em inglês. É a capacidade que uma máquina tem de aprender por conta própria utilizando dados já observados, de maneira que consiga tomar decisões a partir desse aprendizado.
7

![[Pasted image 20250513102201.png]]

Supervised Learning, que significa aprendizado supervisionado em inglês, é uma categoria de algoritmos de Machine Learning. Chamamos esses algoritmos de supervisionados, porque usamos um conjunto de dados que possuem resultados já observados, ou já rotulados, que serão usados para treinar os algoritmos para classificar ou prever resultados com um certo grau de acerto.

O aprendizado supervisionado pode ser subdividido em duas categorias: a Classificação e a Regressão. Na Regressão, o algoritmo tem como objetivo prever um valor contínuo (real), usando dados de input, se baseando em dados históricos (de treino). Na Classificação, o algoritmo tem como objetivo prever uma categoria, usando dados de input, se baseando em dados de treino.

![[Pasted image 20250513102314.png]]
## Aplicações de Algoritmos de Regressão

Em qualquer situação que queremos prever um valor numérico baseado em dados históricos, podemos usar um algoritmo de Regressão. Vejamos algumas aplicações:

- Previsão de demanda de certo produto
- Previsão de do PIB de um país
- Previsão da audiência em um site na Black Friday
- Previsão de preços de barril de petróleo
- Previsão do quanto uma pessoa vai gastar em produtos em um e-commerce

## Aplicações de Algoritmos de Classificação

Toda vez que for necessário classificar um conjunto de dados em categorias já pré-estabelecidas, podemos usar um algoritmo de Classificação. Vejamos algumas aplicações:

- Detecção de Spam em email
- Classificação de Imagem
- Identificação de doenças em exames
- Identificação Biométrica
- Análise de sentimento em imagens ou textos
- Previsão de Churn em clientes
- Detecção de Anomalia - detecção de fraude


![[Pasted image 20250513102456.png]]

-----

![[Pasted image 20250513102649.png]]

### **Aprendizado Não Supervisionado**

O aprendizado não supervisionado é um tipo de machine learning em que os dados não possuem rótulos (labels) predefinidos. O objetivo é **encontrar padrões ou estruturas ocultas** nos dados. Ele se divide principalmente em duas categorias:

1. **Clusterização (Agrupamento)**
    
    - Agrupa dados similares em clusters (grupos).
        
    - Exemplo: Segmentação de clientes em grupos com comportamentos semelhantes.
        
2. **Redução de Dimensionalidade**
    
    - Reduz o número de variáveis (features) mantendo a informação mais relevante.
        
    - Exemplo: Simplificar um conjunto de dados com 1000 colunas para apenas 10, preservando a estrutura principal.

#### **Redução de Dimensionalidade**

É uma técnica que transforma dados de **alta dimensionalidade** (muitas variáveis) em uma representação de **baixa dimensionalidade** (menos variáveis), mantendo o máximo possível da informação original.

#### **Por que é necessária?**

- **Alta dimensionalidade** (muitas variáveis) pode causar:
    
    - **Overfitting**: O modelo se ajusta demais aos dados de treino e performa mal em dados novos.
    
    - **Custo computacional alto**: Mais variáveis exigem mais processamento e memória.
    
    - **Dificuldade de visualização**: Dados com mais de 3 dimensões são difíceis de plotar e interpretar.
    
    - **Correlação e redundância**: Muitas variáveis podem ser repetitivas ou irrelevantes

#### **Técnicas de Redução de Dimensionalidade**

#### **Principal Component Analysis (PCA)**

- Transforma os dados em um novo sistema de coordenadas, onde os primeiros componentes capturam a maior variação.
- Exemplo: Se um dataset tem 100 features, o PCA pode reduzir para 10 componentes principais que explicam 95% da variância.

#### **t-SNE (t-Distributed Stochastic Neighbor Embedding)**

- Focado em **visualização**, preserva a estrutura local (similaridade entre pontos próximos).
- Muito usado para explorar clusters em dados complexos.

#### **Autoencoders (Redes Neurais)**

- Usam redes neurais para comprimir os dados (encoder) e depois reconstruí-los (decoder).
- Útil para dados não lineares (ex.: imagens).


#### Clusterização 
Agrupa dados similares em clusters (grupos) **sem usar rótulos pré-definidos**.

1. **Objetivo**: Encontrar padrões naturais nos dados, agrupando instâncias semelhantes.

2. **Métricas de similaridade**: Usa distâncias (ex.: Euclidiana, Manhattan) ou similaridade (ex.: cosseno) para medir quão "próximos" os dados estão.

3. **Algoritmos**:
    
    - **K-means**: Divide os dados em _K_ grupos, minimizando a variância dentro de cada cluster.
  

Machine learning significa aprendizado de máquina em inglês. É a capacidade que uma máquina tem de aprender por conta própria utilizando dados já observados, de maneira que consiga tomar decisões a partir desse aprendizado.
7

![[Pasted image 20250513102201.png]]

Supervised Learning, que significa aprendizado supervisionado em inglês, é uma categoria de algoritmos de Machine Learning. Chamamos esses algoritmos de supervisionados, porque usamos um conjunto de dados que possuem resultados já observados, ou já rotulados, que serão usados para treinar os algoritmos para classificar ou prever resultados com um certo grau de acerto.

O aprendizado supervisionado pode ser subdividido em duas categorias: a Classificação e a Regressão. Na Regressão, o algoritmo tem como objetivo prever um valor contínuo (real), usando dados de input, se baseando em dados históricos (de treino). Na Classificação, o algoritmo tem como objetivo prever uma categoria, usando dados de input, se baseando em dados de treino.

![[Pasted image 20250513102314.png]]
## Aplicações de Algoritmos de Regressão

Em qualquer situação que queremos prever um valor numérico baseado em dados históricos, podemos usar um algoritmo de Regressão. Vejamos algumas aplicações:

- Previsão de demanda de certo produto
- Previsão de do PIB de um país
- Previsão da audiência em um site na Black Friday
- Previsão de preços de barril de petróleo
- Previsão do quanto uma pessoa vai gastar em produtos em um e-commerce

## Aplicações de Algoritmos de Classificação

Toda vez que for necessário classificar um conjunto de dados em categorias já pré-estabelecidas, podemos usar um algoritmo de Classificação. Vejamos algumas aplicações:

- Detecção de Spam em email
- Classificação de Imagem
- Identificação de doenças em exames
- Identificação Biométrica
- Análise de sentimento em imagens ou textos
- Previsão de Churn em clientes
- Detecção de Anomalia - detecção de fraude


![[Pasted image 20250513102456.png]]

-----

![[Pasted image 20250513102649.png]]

### **Aprendizado Não Supervisionado**

O aprendizado não supervisionado é um tipo de machine learning em que os dados não possuem rótulos (labels) predefinidos. O objetivo é **encontrar padrões ou estruturas ocultas** nos dados. Ele se divide principalmente em duas categorias:

1. **Clusterização (Agrupamento)**
    
    - Agrupa dados similares em clusters (grupos).
    - Exemplo: Segmentação de clientes em grupos com comportamentos semelhantes.
    
2. **Redução de Dimensionalidade**
    
    - Reduz o número de variáveis (features) mantendo a informação mais relevante.
    - Exemplo: Simplificar um conjunto de dados com 1000 colunas para apenas 10, preservando a estrutura principal.

#### **Redução de Dimensionalidade**

É uma técnica que transforma dados de **alta dimensionalidade** (muitas variáveis) em uma representação de **baixa dimensionalidade** (menos variáveis), mantendo o máximo possível da informação original.

#### **Por que é necessária?**

- **Alta dimensionalidade** (muitas variáveis) pode causar:
    
    - **Overfitting**: O modelo se ajusta demais aos dados de treino e performa mal em dados novos.
    
    - **Custo computacional alto**: Mais variáveis exigem mais processamento e memória.
    
    - **Dificuldade de visualização**: Dados com mais de 3 dimensões são difíceis de plotar e interpretar.
    
    - **Correlação e redundância**: Muitas variáveis podem ser repetitivas ou irrelevantes

#### **Técnicas de Redução de Dimensionalidade**

##### **Principal Component Analysis (PCA)**

- Transforma os dados em um novo sistema de coordenadas, onde os primeiros componentes capturam a maior variação.
- Exemplo: Se um dataset tem 100 features, o PCA pode reduzir para 10 componentes principais que explicam 95% da variância.

##### **t-SNE (t-Distributed Stochastic Neighbor Embedding)**

- Focado em **visualização**, preserva a estrutura local (similaridade entre pontos próximos).
- Muito usado para explorar clusters em dados complexos.

##### **Autoencoders (Redes Neurais)**

- Usam redes neurais para comprimir os dados (encoder) e depois reconstruí-los (decoder).
- Útil para dados não lineares (ex.: imagens).


#### Clusterização 
Agrupa dados similares em clusters (grupos) **sem usar rótulos pré-definidos**.

1. **Objetivo**: Encontrar padrões naturais nos dados, agrupando instâncias semelhantes.

2. **Métricas de similaridade**: Usa distâncias (ex.: Euclidiana, Manhattan) ou similaridade (ex.: cosseno) para medir quão "próximos" os dados estão.

3. **Algoritmos**:
- **K-means**: Divide os dados em _K_ grupos, minimizando a variância dentro de cada cluster.

- **DBSCAN**: Agrupa dados baseado em densidade, identificando outliers.

- **Hierárquico**: Cria uma árvore de clusters (dendrograma) para análise multinível.

![[Pasted image 20250513103824.png]]
#### **Outras técnicas**
- LDA (Linear Discriminant Analysis)
- UMAP (Uniform Manifold Approximation and Projection)
- Factor Analysis

Os algoritmos de redução de dimensionalidade, em geral, são utilizados em conjunto com outros algoritmos de machine learning. Já os algoritmos de clusterização possuem aplicações múltiplas, como segmentação de usuários de acordo com seu comportamento, detecção de fraude em seguros, recomendação de conteúdo e até mesmo para servir como uma grande ajuda em uma análise exploratória de dados pouco conhecidos.

![[Pasted image 20250513103954.png]]

E qual a diferença entre os 3 tipos de aprendizado? No aprendizado por reforço, o feedback recebido a cada interação do modelo é utilizado para atualizar o algoritmo, que vai gerar novos resultados. No aprendizado supervisionado, temos um alvo e queremos que o algoritmo acerte o máximo de alvos possíveis, e o modelo aprende de acordo com cada resposta já observada. Já no aprendizado não supervisionado, não há feedback nem resposta, e o algoritmo tenta encontrar padrões de comportamento dentro dos dados.

![[Pasted image 20250513104302.png]]

