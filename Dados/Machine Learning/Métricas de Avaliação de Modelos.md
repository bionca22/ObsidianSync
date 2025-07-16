Vamos falar sobre como podemos medir o quão bom um modelo de machine learning é, ou seja, quais métricas podemos utilizar para medir se um algoritmo, depois de treinado, está desempenhando bem a função para a qual ele será utilizado. A importância desse assunto é grande, pois nos permite não só comparar o desempenho entre modelos com o mesmo objetivo, mas também de entender um valor esperado de comportamento do algoritmo escolhido.

Para avaliar o quão bem está ajustado um modelo aos dados disponíveis, de forma que o modelo cumpra o papel esperado, devemos considerar a natureza de seu objetivo. Isso significa que para avaliar um modelo de recomendação utilizaremos uma métrica e, para um modelo de classificação, utilizaremos outra.

Dessa forma, para cada tipo de modelo de machine learning, teremos diferentes métricas para medir aspectos diferentes do ajuste do modelo. Vamos ver a seguir algumas delas:

**Matriz de Confusão**

A matriz de confusão é a forma mais simples de visualizar uma performance de um modelo de classificação. Ela indica quantos resultados foram falso-positivos, falso-negativos, verdadeiro-positivos ou verdadeiro-negativos.

O projeto open source scikit-learn já possui a implementação da [matriz de confusão](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.confusion_matrix.html).

![[Pasted image 20250520173928.png]]

**Acurácia**

A acurácia é a métrica que dá a porcentagem de classificações corretas no dataset. Por exemplo, se temos 1000 observações, onde temos que classificá-las em 2 classes, e o classificador acertou 950 previsões, a acurácia seria de 95%.

O projeto open source scikit-learn já possui a implementação da [acurácia](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.accuracy_score.html).

**Acurácia = TP + TN / (TP + TN + FP + FN)**

Onde:

- TP = Verdadeiros Positivos
- TN = Verdadeiros Negativos
- FP = Falsos Positivos
- FN = Falsos Negativos

a Acurácia é simples e trás números altos de precisão, mas em casos específicos como a detecção de doenças raras o modelo deixa a desejar. Mas para isso existem opções como **Precision & Recall** 


**Precision & Recall**

A precisão é uma métrica que dá um foco nos positivos. Ela responde a seguinte pergunta: das observações que classificamos como positivas, quantas realmente foram positivas?

O recall, também chamado de sensibilidade, dá uma maior ênfase nos negativos. Ele responde a seguinte pergunta: de todas as observações que são positivas, quantas foram classificadas como positivas? Ela é muito relevante quando temos classes com menos observações de treino do que outras.

O projeto open source scikit-learn já possui a implementação da [precisão e do recall](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.precision_recall_fscore_support.html).

![[Pasted image 20250520174740.png]]

**F1-Score**

O F1-Score é uma média harmônica entre a precisão e o recall. É uma forma de olhar para somente uma métrica para avaliar o modelo. Uma vantagem dessa métrica é que, se a precisão for muito baixa, o F1-score também será baixo. O mesmo vale para o recall.

O projeto open source scikit-learn já possui a implementação da [f1-score](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.f1_score.html). Além disso, possui uma visão geral de [métricas de avaliação de modelos de classificação](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.classification_report.html), que traz tanto o f1-score quanto o precision e o recall.

![[Pasted image 20250520175209.png]]

**F1 score = 2 * (recall * precision) / (recall + precision)**

Para modelos de classificação que determinam uma probabilidade de uma observação pertencer a uma classe, se faz necessário definir um threshold que indique que tal observação será daquela classe, se obtiver uma probabilidade maior do que o threshold definido. Muitas vezes, determinados como 50%, mas pode ser que outros valores gerem resultados melhores.

**Curva ROC**

A curva ROC (Receiver Operating Characteristic) é utilizada para avaliar a performance do algoritmo de classificação para diferentes thresholds de classificação. Ela é feita utilizando a taxa de falsos positivos e a taxa de verdadeiros positivos, para cada valor de threshold.

![[Pasted image 20250520175600.png]]

Assim, quanto maior a área abaixo da curva, melhor o ajuste do modelo. Por isso, temos a métrica AUC (área under the curve, ou seja, área abaixo da curva) para medir esse ajuste.

O projeto open source scikit-learn já possui a implementação da [curva ROC e do AUC](https://scikit-learn.org/stable/auto_examples/model_selection/plot_roc.html).

----

**Clusterização**

**Silhouette Score**

O Silhouette Score é usado para medir a distância de separação entre os clusters. Ele é uma medida que indica quão próxima cada observação em um cluster está das observações nos clusters vizinhos. Esse score está sempre em um intervalo entre -1 e 1, além de ser muito utilizado para encontrar a quantidade ideal de clusters em um algoritmo de clusterização.

O Silhouette Score é calculado usando a distância média intra-cluster (a) e a distância média do cluster mais próximo (b) para cada amostra. O coeficiente de silhueta para uma amostra é (b−a)/max(b,a)(b−a)/max(b,a), onde **b** é a distância média entre cada observação e o cluster mais próximo do qual a observação não faz parte, e a é a distância média dentro de cada cluster.

O projeto open source scikit-learn já possui a implementação do [silhouette score](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.silhouette_score.html).

![[Pasted image 20250520180014.png]]

Quanto maior o coeficiente (mais próximo de 1), mais distantes estão as observações de um cluster das observações dos clusters vizinhos. O valor 0 vai indicar que os clusters estão muito próximos, quase se misturando. Quanto mais próximo de -1, maior a chance de uma observação ter sido classificada no cluster errado.

O silhouette score será a média dos coeficientes de silhueta de todos os clusters e o usaremos para avaliar o quão boa foi a clusterização.

![[Pasted image 20250520180421.png]]
aqui 2 seria a melhor quantidade de clusters

**Recomendação**

**MRR**

Essa é uma métrica boa para medir se o melhor item para um usuário está sendo mostrado na melhor posição. Ele tenta avaliar se o item mais relevante está com o melhor ranking.

O projeto open source scikit-learn já possui a implementação do [silhouette score](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.silhouette_score.html).

![[Pasted image 20250520180644.png]]

![[Pasted image 20250520180708.png]]
 Os verdes seriam as localizações no trilho, então demonstra os resultados levando em conta também o posicionamento da sugestão.
 
-----
**MAP**

Com o MAP (mean average precision, em inglês), o objetivo é dar um peso maior para os erros do início da lista e um peso menor para os do fim da lista. Ou seja, ela também leva em consideração a ordem em que está o item relevante. Ao contrário do MRR, ela leva em conta que o usuário pode ter mais de um item relevante em sua lista de recomendações.

![[Pasted image 20250520180814.png]]
aqui é levado em conta, além da posição da sugestão escolhida, a quantidade de recomendações que foram escolhidas mediante o peso da posição.

----
### Teste A/B

**Modelos em produção**

E agora que o seu modelo está em produção, qual a melhor forma de avaliar se ele está com uma boa performance? Com testes A/B! Através do teste A/B, podemos provar a causalidade de forma mais segura e confiável e, por isso, é a melhor opção para entender a performance de um modelo de machine learning.

![[Pasted image 20250520181428.png]]

A melhor métrica que você pode escolher é a métrica que seu negócio está tentando melhorar. Seu modelo de machine learning, antes de tudo, tem um objetivo de negócio, e uma métrica para quantificar se esse objetivo de negócio está sendo alcançado é a métrica ideal para avaliar a performance do seu modelo.

![[Pasted image 20250520181517.png]]

![[Pasted image 20250520181609.png]]

**Como aplicar na prática o que aprendeu**

Toda vez que você estiver utilizando um modelo de machine learning, será preciso avaliar o quão bom foi o ajuste do modelo. Por isso, é importante ter as métricas apropriadas à disposição para cada tipo de modelo.

Portanto, da próxima vez que testar um modelo, procure avaliar o ajuste utilizando as métricas aprendidas. Além disso, é essencial que, quando o modelo for utilizado em produção, seja possível a medição de seu desempenho com métricas ligadas ao problema que está tentando ser resolvido.

**Tópicos avançados**

Existem várias métricas de avaliação de modelos de classificação, **clusterização** e **recomendação**. Cada uma delas vai medir um aspecto diferente da performance do modelo. Além disso, em várias ocasiões, vale a pena analisar mais de uma métrica para entender diferentes nuances do modelo.

Seguem sugestões de leituras:

[https://towardsdatascience.com/performance-metrics-in-machine-learning-part-3-clustering-d69550662dc6](https://towardsdatascience.com/performance-metrics-in-machine-learning-part-3-clustering-d69550662dc6)

[https://medium.com/swlh/rank-aware-recsys-evaluation-metrics-5191bba16832](https://medium.com/swlh/rank-aware-recsys-evaluation-metrics-5191bba16832)