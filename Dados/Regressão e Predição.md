
#### Regressão Linear          
 
fatores básicos estão sempre associados a uma variável dependente e uma independente. é necessário descobrir o coeficiente angular 

openrefine >> https://openrefine.org/


Todo modelo de regressão linear parte de duas vertentes principais: uma variável independente e uma variável dependente. Então, tem-se uma função de primeiro grau

**_Variável independente:_** tem-se um valor que vai influenciar diretamente o que se deseja encontrar. Temos como exemplo uma previsão de vendas de roupas, precisamos compreender as estações dos anos e quais vão interferir nestas vendas (sazonalidade).

**_Variável dependente:_** Já essa variável é aquela que desejamos prever, ou seja, ela depende de outros valores. No exemplo que demos acima, seria identificar as vendas das nossas peças de roupas.

Estas variáveis estão associadas, diretamente, a uma fórmula simples:

f(x)=a+bxf(x)=a+bx

Onde temos como a um valor que intercepta nosso eixo y, b nosso coeficiente angular e x nossa variável independente. Com isso, podemos obter uma perspectiva futura como análise de previsão, a partir do aprendizado de máquina.

Um objetivo de um modelo de aprendizagem de máquina que utiliza a regressão linear é, a partir de um dado conjunto de dados, entender o padrão destes dados e se estes podem ser descritos e analisados a partir de uma função de primeiro grau (correspondente a regressão linear e como verificado na fórmula 1).

Vejamos um exemplo básico para compreensão da utilização de regressão linear. Vamos pensar que desejamos saber o preço de aluguel de terminado imóvel. Para este caso uma variável dependente (número de quartos). A definição do preço do aluguel se dá exatamente pelo número de quartos. O preço fixo a ser pago é de 300 reais, mais a variação do número de quartos (a cada quarto há uma estimativa de aumento de 250 reais). Assim, fica fácil modelar esse problema, onde

Figura 1: Exemplo de regressão linear
![[Pasted image 20250527184620.png]]

Neste sentido e, especialmente de aprendizagem de máquina, um modelo de regressão linear segue a seguinte estrutura (Figura 2)

![[Pasted image 20250527184706.png]]

Associado à regressão linear, também há métricas de avaliação de problemas. As mais comuns são:

**_Mean absolute error_** **(MAE) que corresponde ao erro médio absoluto:**  é a média do valor absoluto dos erros (Equação 2)

![[Pasted image 20250527185808.png]]

**_Mean Squared Error (MSE_****) que corresponde ao erro médio quadrático**: é a média dos erros quadrados (Equação 3)

![[Pasted image 20250527185832.png]]

**_Root Mean Square Error (RMSE) que corresponde a raiz do erro quadrático médio:_** é a raiz quadrada da média dos erros quadrados (Equação 4):

![[Pasted image 20250527185854.png]]

Comparando estas métricas:

- MAE é corresponde ao erro médio;
- MSE é mais popular que o MAE, porque a MSE "puniria" erros maiores, o que tende a ser útil no mundo real.
- RMSE é ainda mais popular do que MSE, porque o RMSE é interpretável nas unidades "y".

Considerando a implementação de regressão linear como um algoritmo de aprendizagem de máquina, a linguagem de programação Python traz importantes bibliotecas que contribuem para esse processo, como é o caso do _Pandas, Numpy, matploitlib e sklearn._ Estas são bibliotecas que permitem a análise de dados e a verificação do padrão de comportamento destes dados, bem como a implementação de algoritmos de aprendizagem de máquina (como é o caso do algoritmo de regressão linear), possibilitando uma maneira mais prática e completa de aplicação de aprendizagem de máquina. As mais relevantes são:

**_Pandas_**

Esta é uma biblioteca em Python que permite trabalhar com diversos tipos de dados, desde dados tabulares, dados ordenados, matrizes ou qualquer outro tipo de dados que não precisam estar rotulados.

**_Scikit Learn_**

Já a _Scikit learn_ é uma biblioteca de aprendizagem de máquina que providencia o treino de várias técnicas de estatísticas e _machine learning_. Funciona tanto para aprendizagem supervisionada quanto para não supervisionada

**Tópicos avançados**

Dentre os pontos centrais do conteúdo ministrado, o mais relevante está associado com a compreensão da regressão e da regressão linear. Compreender seu funcionamento e identificar padrões de dados torna-se o primeiro passo para a definição do modelo mais apropriado para qualquer base de dados e, consequentemente, do problema. Desta forma, como conteúdo bônus tem-se um link que providencia uma visão geral de estimativas em regressão linear, trazendo, inclusive, práticas que evidenciam a sua utilização. Vamos lá?

KHAN ACADEMY. Estimativas com regressão linear. Disponível em: <[https://pt.khanacademy.org/math/statistics-probability/describing-relationships-quantitative-data/introduction-to-trend-lines/v/example-estimating-from-regression-line](https://pt.khanacademy.org/math/statistics-probability/describing-relationships-quantitative-data/introduction-to-trend-lines/v/example-estimating-from-regression-line)>. Acesso em: 30 de nov. 2022.


---


# Regressão Logística e outros tipos de regressões

Para começarmos nosso resumo, vamos compreender a regressão não linear. De modo geral, a regressão não linear é um modelo matemático que ajusta uma equação a determinados dados usando uma linha gerada. Como é o caso de uma regressão linear que usa uma equação de linha reta (como f(x) = a + bx), a regressão não linear mostra associação usando uma curva, tornando-a não linear no parâmetro.

Um modelo de regressão não linear simples é expresso da seguinte forma:

Y = f(X,β) + ε

Onde:

**X** é um vetor de preditores P

**β** é um vetor de k parâmetros

**F (-)** é a função de regressão conhecida

**ε** é o termo de erro

Alternativamente, o modelo também pode ser escrito da seguinte forma:

Yi = h [xi(1) , xi(2), … , xi(m) ; Ѳ1, Ѳ2, …, Ѳp] + Ei

Onde:

**Yi** é a variável responsiva;

**h** é a função;

**x** é a entrada;

**Ѳ** é o parâmetro a ser estimado.

Como cada parâmetro pode ser avaliado para determinar se é não linear ou linear, uma determinada função Yi pode incluir uma mistura de parâmetros não lineares e lineares. A função h no modelo é considerada, pois não pode ser escrita como linear nos parâmetros. Em vez disso, a função é deduzida da teoria.

O termo “não linear” refere-se aos parâmetros do modelo, em oposição às variáveis independentes. Existem possibilidades ilimitadas para descrever a parte determinística do modelo. Essa flexibilidade fornece uma boa base para fazer inferências estatísticas.

O objetivo do modelo é minimizar a soma dos quadrados o mínimo possível usando procedimentos numéricos iterativos. A melhor estimativa para os parâmetros do modelo é o princípio dos mínimos quadrados, que mede quantas observações se desviam da média do conjunto de dados. Também é importante notar que a diferença entre os modelos de regressão linear e não linear está no cálculo dos mínimos quadrados.

Já com relação a regressão logística, é um algoritmo de aprendizado de máquina supervisionado que realiza tarefas de classificação binária prevendo a probabilidade de um resultado, evento ou observação. O modelo fornece um resultado binário ou dicotômico limitado a dois resultados possíveis: sim/não, 0/1 ou verdadeiro/falso.

A regressão lógica analisa a relação entre uma ou mais variáveis ​​independentes e classifica os dados em classes discretas. É amplamente utilizado em modelagem preditiva, onde o modelo estima a probabilidade matemática de uma instância pertencer a uma categoria específica ou não.

Por exemplo, 0 – representa uma classe negativa; 1 – representa uma classe positiva. A regressão logística é comumente usada em problemas de classificação binária em que a variável de resultado revela uma das duas categorias (0 e 1).

A regressão logística usa uma função logística chamada função sigmóide para mapear previsões e suas probabilidades. A função sigmóide refere-se a uma curva em forma de S que converte qualquer valor real em um intervalo entre 0 e 1.

A função _sigmóide_ é referida como uma função de ativação para a regressão logística e é definida como:

![[Pasted image 20250527202103.png]]

Onde,

**e =** base dos logaritmos naturais

**x =** valor numérico que se deseja transformar

A equação a seguir representa a regressão logística:

![[Pasted image 20250527202124.png]]

Onde:

**x** = valor de entrada

**y** = saída prevista

**b0** = viés ou termo de interceptação

**b1** = coeficiente para entrada (x)

Essa equação é semelhante à regressão linear, em que os valores de entrada são combinados linearmente para prever um valor de saída usando pesos ou valores de coeficiente. No entanto, ao contrário da regressão linear, o valor de saída modelado aqui é um valor binário (0 ou 1) em vez de um valor numérico.

A regressão logística pode ser utilizada a partir da linguagem de programação Python, dentro da biblioteca _Sklearn_

**Tópicos avançados**

A regressão logística é uma importante ferramenta para classificação e predição dentro de aprendizagem de máquina. Que tal ver na prática como isso acontece? Neste link tem um passo a passo da utilização de regressão logística. Vamos lá?

Para saber mais informações, acessar esse link:

STANKEVIX, G. Regressão Logística em R e Python (PyTools). Disponível em: < [https://medium.com/@gabriel.stankevix/regress%C3%A3o-log%C3%ADstica-em-r-e-python-pytools-9f4eba2061a1](https://medium.com/@gabriel.stankevix/regress%C3%A3o-log%C3%ADstica-em-r-e-python-pytools-9f4eba2061a1)>. Acesso em: 30 de nov. 2022

Caro estudante, você consegue acessar os códigos utilizados na disciplina no link a seguir: [https://github.com/FaculdadeDescomplica/RegressaoePredicao](https://github.com/FaculdadeDescomplica/RegressaoePredicao)

---
# Arvore de Regressão

**Resumo**

Vamos começar nosso resumo falando sobre a árvore de decisão. Uma árvore de decisão é um tipo específico de fluxograma usado para visualizar o processo de tomada de decisão, mapeando diferentes cursos de ação, bem como seus possíveis resultados. As árvores de decisão geralmente consistem em três elementos diferentes:

**_Nó Raiz:_**

O nó de nível superior representa o objetivo final ou a grande decisão que você está tentando tomar.

**_Galhos:_**

Ramos, que se originam da raiz, representam diferentes opções – ou cursos de ação – que estão disponíveis ao tomar uma decisão específica. Eles são mais comumente indicados com uma linha de seta e geralmente incluem custos associados, bem como a probabilidade de ocorrer.

**_Nó da folha:_**

Os nós das folhas – que são anexados ao final das ramificações – representam possíveis resultados para cada ação. Normalmente existem dois tipos de nós folha: nós folha quadrados, que indicam outra decisão a ser tomada, e nós folha circulares, que indicam um evento casual ou resultado desconhecido.

Elas são divididas em dois tipos principais: categóricas e contínuas. Na primeira há inclusão de variáveis, chamadas de variáveis de destino, em categorias. Essas categorias são definidas a priori e há um aspecto limitante nestas categorias definidas. Já a segunda está associada como uma variável que terá seu destino contínuo. Por exemplo, se não se sabe a renda de determinada família, esta renda pode ser identificada a partir de outra informação, como idade, cargo, dentre outras.

![[Pasted image 20250603083117.png]]

E por que utilizamos árvores de decisão?

Primeiro porque as árvores de decisão são flexíveis, possibilitando mais flexibilidade para explorar, planejar e prever vários resultados possíveis para suas decisões, independentemente de quando elas realmente ocorrerem.

Por exemplo, pode-se utilizar árvores de decisão para identificar crescimento de negócios baseando-se em dados históricos obtidos por organizações ao longo dos anos. Por outro lado, pode-se utilizar árvores de decisão para encontrar potenciais clientes a partir de dados demográficos. Por ser um algoritmo de aprendizagem de máquina, há diversos cenários em que pode-se utilizar árvores de decisão.

Além disso, as árvores de decisão demonstram visualmente as relações de causa e efeito, fornecendo uma visão simplificada de um processo potencialmente complicado. As árvores de decisão também são diretas e fáceis de entender, mesmo que você nunca tenha criado uma antes, fornecendo uma visão equilibrada do processo de tomada de decisão, enquanto calculam o risco e a recompensa.

Uma árvore de decisão para ajudar alguém a determinar se deve alugar ou comprar, por exemplo, seria um conteúdo bem-vindo em um blog imobiliário. Você também pode criar uma árvore de decisão personalizada para ajudar seus clientes a determinar qual propriedade é melhor para eles.

Já as florestas aleatórias têm como finalidade a resolução de problemas de regressão e classificação, utilizando três hiperparâmetros: tamanho do nó, número de árvores e número dos recursos de determinada amostra. No fim das contas, uma floresta aleatória é composta de diversas árvores de decisão.

![[Pasted image 20250603083639.png]]

Ambas podem ser aplicadas a partir da biblioteca Sklearn da linguagem de programação Python.

No caso das árvores de decisão, sua aplicação acontece da seguinte maneira:

**from** **sklearn.tree** **import** **DecisionTreeClassifier**

Onde a partir da importação da biblioteca Sklearn, basta realizar a segunda importação do Classificador de Árvore de Decisão.

No caso das florestas aleatórias, sua aplicação acontece da seguinte maneira:

**from** **sklearn.ensemble** **import** **RandomForestClassifier**

Onde a partir da importação da biblioteca Sklearn, basta realizar a segunda importação do Classificador de Floresta de Decisão.

SKLEARN. Compreendendo a biblioteca SKLEARN Disponível em: < [https://scikit-learn.org/stable/](https://scikit-learn.org/stable/)>. Acesso em: 30 de nov. 2022

# Treinamento, Validação e Testes

**Resumo**

Os modelos de classificação são usados em problemas de classificação para prever a classe de destino da amostra de dados. O modelo de classificação prevê a probabilidade de cada instância pertencer a uma classe ou outra. É importante avaliar o desempenho do modelo de classificação para usar esses modelos de forma confiável na produção para resolver problemas do mundo real. As medidas de desempenho em modelos de classificação de aprendizado de máquina são usadas para avaliar o desempenho dos modelos de classificação de aprendizado de máquina em um determinado contexto. Essas métricas de desempenho incluem exatidão, precisão, recall e acurácia. Como nos ajuda a entender os pontos fortes e as limitações desses modelos ao fazer previsões em novas situações, o desempenho do modelo é essencial para o aprendizado de máquina.

Vamos começar falando sobre a precisão. A pontuação de precisão do modelo mede a proporção de rótulos previstos positivamente que estão realmente corretos. A precisão também é conhecida como valor preditivo positivo. A precisão é usada em conjunto com o recall para compensar falsos positivos e falsos negativos. A precisão é afetada pela distribuição de classes. Se houver mais amostras na classe minoritária, a precisão será menor. A precisão pode ser pensada como uma medida de exatidão ou qualidade. Se quisermos minimizar falsos negativos, escolheríamos um modelo com alta precisão, por outro lado, se quisermos minimizar os falsos positivos, escolheríamos um modelo com alto recall.

A precisão é usada principalmente quando precisamos prever a classe positiva e há um custo maior associado a falsos positivos do que a falsos negativos, como em diagnósticos médicos ou filtragem de spam. Por exemplo, tem apenas 50% de precisão, isso significa que metade das vezes que ele prevê que um e-mail é spam, na verdade não é spam.

**_Pontuação de precisão = TP / (FP + TP)_**

A partir da fórmula acima, você pode notar que o valor de falso-positivo afetaria a pontuação de precisão. Assim, ao construir modelos preditivos, você pode optar por se concentrar adequadamente para construir modelos com falsos positivos mais baixos se uma alta pontuação de precisão for importante para os requisitos do cenário.

Agora vamos falar de Recall. A pontuação de recall do modelo representa a capacidade do modelo de prever corretamente os positivos dos positivos reais. Isso é diferente da precisão, que mede quantas previsões feitas pelos modelos são realmente positivas de todas as previsões positivas feitas. Por exemplo: se seu modelo de aprendizado de máquina estiver tentando identificar avaliações positivas, a pontuação de recall seria a porcentagem dessas avaliações positivas que seu modelo de aprendizado de máquina previu corretamente como positivas. Em outras palavras, mede a qualidade do nosso modelo de aprendizado de máquina em identificar todos os positivos reais de todos os positivos que existem em um conjunto de dados. Quanto maior a pontuação de recall, melhor o modelo de aprendizado de máquina identifica exemplos positivos e negativos.

A recall também é conhecida como sensibilidade ou taxa de verdadeiros positivos. Uma alta pontuação de recordação indica que o modelo é bom em identificar exemplos positivos. Por outro lado, uma baixa pontuação de recordação indica que o modelo não é bom para identificar exemplos positivos.

A recall é frequentemente usada em conjunto com outras métricas de desempenho, como precisão e exatidão, para obter uma imagem completa do desempenho do modelo. Matematicamente, representa a proporção de verdadeiro positivo para a soma de verdadeiro positivo e falso negativo.

**Pontuação de Recall = TP / (FN + TP)**

A partir da fórmula acima, você pode notar que o valor de falso-negativo afetaria a pontuação de recall. Assim, ao construir modelos preditivos, você pode optar por se concentrar adequadamente para construir modelos com falsos negativos mais baixos se uma alta pontuação for importante para os requisitos do cenário.

Agora vamos compreender acurácia. A acurácia do modelo é uma métrica de desempenho do modelo de classificação de aprendizado de máquina que é definida como a proporção de verdadeiros positivos e verdadeiros negativos para todas as observações positivas e negativas. Em outras palavras, a acurácia nos diz com que frequência podemos esperar que nosso modelo de aprendizado de máquina preveja corretamente um resultado do número total de vezes que ele fez previsões. Por exemplo: vamos supor que você estava testando seu modelo de aprendizado de máquina com um conjunto de dados de 100 registros e que seu modelo de aprendizado de máquina previu todas as 90 dessas instâncias corretamente. A métrica de precisão, neste caso, seria: (90/100) = 90%. A taxa de precisão é ótima, mas não nos diz nada sobre os erros que nossos modelos de aprendizado de máquina cometem em novos dados que não vimos antes.

Matematicamente, representa a razão da soma dos verdadeiros positivos e verdadeiros negativos de todas as previsões.

**Pontuação de acurácia = (TP + TN)/ (TP + FN + TN + FP)**

De modo geral, a biblioteca do Python, Sklearn fornece estes testes com a finalidade de identificação do desempenho do algoritmo em determinada base de dados, como ilustra a Figura 1 abaixo.

![[Pasted image 20250603103057.png]]

**Tópicos avançados**

Que tal saber mais sobre os testes para identificação do desempenho de algoritmos de aprendizagem de máquina? No link abaixo há várias informações sobre os diferentes modos de aplicação destes testes e como estes testes podem contribuir para identificar o desempenho de qualquer algoritmo em qualquer base de dados. Legal, né?

Para saber mais informações, acessar esse link:

MARIANO, D.. Métricas de avaliação em machine learning. Disponível em: <[https://bioinfo.com.br/metricas-de-avaliacao-em-machine-learning-acuracia-sensibilidade-precisao-especificidade-e-f-score/](https://bioinfo.com.br/metricas-de-avaliacao-em-machine-learning-acuracia-sensibilidade-precisao-especificidade-e-f-score/)> Acesso em: 30 de nov. 2022

----
# Testes de Hipóteses

O teste de hipótese é um tipo de análise estatística em que você testa suas suposições sobre um parâmetro populacional. É usado para estimar a relação entre 2 variáveis estatísticas.

Vamos discutir alguns exemplos de hipóteses estatísticas da vida real:

- Um professor supõe que 10% dos alunos de sua faculdade vêm de famílias de classe alta.
- Um médico acredita que o tratamento contra a obesidade é 40% eficaz para pacientes diabéticos.

Agora que você conhece o teste de hipótese, veja os dois tipos de teste de hipótese em estatística.

A hipótese nula é a suposição de que o evento não ocorrerá. Uma hipótese nula não tem influência sobre o resultado do estudo, a menos que seja rejeitada.

**_H0_** é o símbolo para isso, e é pronunciado H-nula.

A hipótese alternativa é o oposto lógico da hipótese nula. A aceitação da hipótese alternativa segue a rejeição da hipótese nula. H1 é o símbolo para isso.

Vamos entender isso com um exemplo.

Um fabricante de desinfetante afirma que seu produto mata 45% dos germes em média.

Para testar a afirmação dessa empresa, crie uma hipótese nula e alternativa.

**_H0 (Hipótese Nula): Média = 95%._**

**_Hipótese alternativa (H1): A média é inferior a 95%._**

Outro exemplo direto para entender esse conceito é determinar se uma moeda é cara ou coroa. A hipótese nula afirma que a probabilidade de dar cara é igual à probabilidade de dar coroa. Em contraste, a teoria alternativa afirma que a probabilidade de uma exibição de caras e coroas seria muito diferente.

Dependendo da distribuição da população, você pode classificar a hipótese estatística em dois tipos.

**_Hipótese Simples: Uma hipótese simples especifica um valor exato para o parâmetro._**

**_Hipótese composta: Uma hipótese composta especifica um intervalo de valores._**

Exemplo:

A empresa afirma que suas vendas médias para este trimestre são de 1.000 unidades. Este é um exemplo de uma hipótese simples.

Suponha que a empresa afirme que as vendas estão na faixa de 900 a 1.000 unidades. Então este é um caso de hipótese composta.

**_Nível de significância_**

O valor alfa é um critério para determinar se uma estatística de teste é estatisticamente significativa. Em um teste estatístico, Alfa representa uma probabilidade aceitável de um erro Tipo I. Como a alfa é uma probabilidade, pode estar entre 0 e 1. Na prática, os valores de alfa mais comumente usados são 0,01, 0,05 e 0,1, que representam 1%, 5% e 10% de chance de um erro Tipo I , respectivamente (ou seja, rejeitar a hipótese nula quando ela é de fato correta).

**_Valor P_**

Um valor-p é uma métrica que expressa a probabilidade de uma diferença observada ter ocorrido por acaso. À medida que o valor-p diminui, a significância estatística da diferença observada aumenta. Se o valor-p for muito baixo, você rejeita a hipótese nula.

Vamos verificar um exemplo. Neste exemplo, você está tentando testar se a nova campanha publicitária aumentou as vendas do produto. O valor-p é a probabilidade de que a hipótese nula, que afirma que não há mudança nas vendas devido à nova campanha publicitária, seja verdadeira. Se o valor-p for 0,30, então há 30% de chance de que não haja aumento ou diminuição nas vendas do produto. Se o valor-p for 0,03, então há uma probabilidade de 3% de que não haja aumento ou diminuição no valor das vendas devido à nova campanha publicitária. Como você pode ver, quanto menor o valor-p, as chances de a hipótese alternativa ser verdadeira aumentam, o que significa que a nova campanha publicitária causa um aumento ou diminuição nas vendas.

Que tal saber mais sobre o teste de hipóteses? Entender como estes funcionam e os tipos existentes são fundamentais para aplicação em análises estatísticas. No link abaixo há várias informações sobre os diferentes modos de aplicação e como este teste contribui para a testagem de suposições sobre determinado parâmetro populacional. Legal, né?

Para saber mais informações, acessar esse link:

KHAN ACADEMY. Testes de Hipóteses. Disponível em: < [https://pt.khanacademy.org/math/statistics-probability/significance-tests-one-sample/idea-of-significance-tests/v/simple-hypothesis-testing](https://pt.khanacademy.org/math/statistics-probability/significance-tests-one-sample/idea-of-significance-tests/v/simple-hypothesis-testing) >.

---
# Máquina de vetores de suporte (SVM)

**Resumo**

Vamos começar nosso resumo falando sobre Support Vector Machine. Um Support Vectro Machine. Uma máquina de vetor de suporte (SVM) é um algoritmo de aprendizado de máquina que usa modelos de aprendizado supervisionado para resolver problemas complexos de classificação, regressão e detecção de outliers, realizando transformações de dados ideais que determinam limites entre pontos de dados com base em classes, rótulos ou saídas predefinidas. Os SVMs são amplamente adotados em disciplinas como assistência médica, processamento de linguagem natural, aplicativos de processamento de sinal e campos de reconhecimento de fala e imagem.

Tecnicamente, o objetivo principal do algoritmo SVM é identificar um hiperplano que separe distintamente os pontos de dados de diferentes classes. O hiperplano está localizado de tal maneira que a maior margem separa as classes consideradas.

SVMs são potencialmente projetados para problemas de classificação binária. No entanto, com o aumento de problemas multiclasse computacionalmente intensivos, vários classificadores binários são construídos e combinados para formular SVMs que podem implementar tais classificações multiclasse através de meios binários.

No contexto matemático, um SVM refere-se a um conjunto de algoritmos de ML que usam métodos de kernel para transformar recursos de dados empregando funções de kernel. As funções do kernel dependem do processo de mapeamento de conjuntos de dados complexos para dimensões superiores de uma maneira que facilite a separação de pontos de dados. A função simplifica os limites de dados para problemas não lineares adicionando dimensões mais altas para mapear pontos de dados complexos.

Ao introduzir dimensões adicionais, os dados não são totalmente transformados, pois podem atuar como um processo computacionalmente desgastante. Esta técnica é geralmente referida como o truque do kernel, em que a transformação de dados em dimensões superiores é alcançada de forma eficiente e barata.

Vamos ver em detalhes o funcionamento de um algoritmo de support vector machine. Considere a seguinte imagem:

![[Pasted image 20250603140900.png]]

A imagem representa a aparência de um classificador SVM ideal quando o visualizamos em um plano 2-d. Existem duas classes: negativa e positiva, marcadas com as cores vermelha e azul, respectivamente. A razão exata para marcá-los como negativos e positivos será muito mais evidente daqui para frente. O SVM cria um plano em recursos bidimensionais e um hiperplano em recursos multidimensionais chamados de limite de decisão.

O hiperplano separa os recursos e ajuda na classificação do novo ponto de dados de entrada com base em seus valores. Existem n-número de hiperplanos possíveis que podem ser gerados, que podem separar as classes e encontrar o ideal? É aí que os vetores de margem e suporte entram em ação.

Quando o hiperplano para o limite de decisão é gerado, ele também gera dois hiperplanos chamados planos marginais, que são precisamente paralelos ao limite de decisão de forma que ambos os planos marginais passem por pelo menos um dos pontos mais próximos da respectiva classe. Esses pontos mais próximos pelos quais passam os dois planos marginais são chamados de vetores de suporte.

O limite de decisão ótimo é aquele que possui a distância máxima entre dois hiperplanos marginais paralelos, a distância entre eles é conhecida como margem. Portanto, o algoritmo SVM trabalha para maximizar a margem.

Existem dois tipos de problemas de classificação relativos à distribuição de dados: linearmente separáveis e não linearmente separáveis. Dois conjuntos são linearmente separáveis se existe pelo menos uma reta no plano com todos os pontos azuis de um lado da reta e todos os pontos vermelhos do outro lado.

Quando os pontos de dados não podem ser separados por uma linha reta ou um hiperplano reto, esses tipos são conhecidos como não linearmente separáveis. Em tal situação, os kernels SVM atuam e convertem a dimensão baixa em uma dimensão alta, de modo que os pontos de dados sejam linearmente separáveis.

Já na linguagem de programação Python, basta utilizar a biblioteca Sklearn para importar um algoritmo de SVM, como ilustra a imagem abaixo:

![[Pasted image 20250603140933.png]]


**Tópicos avançados**

Que tal saber mais sobre algoritmos de aprendizagem de máquina? Entender como estes funcionam e os tipos existentes são fundamentais para aplicação em análises de predição e classificação. No link abaixo há várias informações sobre os diferentes modos de aplicação e como estes algoritmos podem contribuir para outras áreas, como é o caso de reconhecimento fácil. Legal, né?

Para saber mais informações, acessar esse link:

KHAN ACADEMY. Machine learning algoritmos. Disponível em: < [https://www.khanacademy.org/computing/ap-computer-science-principles/data-analysis-101/x2d2f703b37b450a3:machine-learning-and-bias/a/machine-learning-algorithms](https://www.khanacademy.org/computing/ap-computer-science-principles/data-analysis-101/x2d2f703b37b450a3:machine-learning-and-bias/a/machine-learning-algorithms)>. Acesso em: 30 de nov. 2022

-----
## Transferência de Aprendizagem e Reconhecimento de Voz

**Resumo**

O aprendizado por transferência de aprendizagem (_transfer learning_ – TL) é o processo de aproveitar recursos de uma rede treinada anteriormente para uma dada tarefa em uma outra tarefa parecida. Para que esta definição fique mais clara, vamos expor a seguinte situação: temos poucas imagens de cachorro e sabemos que treinar uma rede do zero é muito trabalhoso e provavelmente não vai funcionar muito bem, porém, conhecemos uma rede muito boa para detectar gatos. Então, podemos seguir o seguinte raciocínio: “cachorros e gatos têm várias características semelhantes, por exemplo, ambos têm 4 patas, rabo, focinho, pelos, entre outras. Então, de alguma forma pode ser aproveitada essa rede treinada de gatos para achar os cachorros do meu problema”.

Para o funcionamento da TL, a rede similar já treinada é utilizada, substituindo a última camada (camada de saída) e adicionando uma camada com a quantidade de neurônios necessários ao nosso problema. Com isso, somente esta nova camada será treinada, o restante da rede não será afetado pelo algoritmo de treinamento.

O TL pode ser aplicado em três situações. Quando os dados das duas tarefas são do mesmo tipo: não adianta utilizar uma rede treinada com imagens para aplicar em dados de voz. Quando a tarefa original foi treinada com muito mais dados do que você tem: imagine que você quer treinar uma rede para detectar uma única raça de cachorros e tem uma rede original que consegue detectar todos os tipos de cachorro. E por fim, quando o domínio dos dados é parecido: no caso de haver características em comum entre os dados, como o caso citado dos cachorros e gatos, não dá para utilizar uma rede treinada com cachorros para reconhecer carros.

A Figura 1 (em inglês) mostra o processo de TL, onde temos o primeiro modelo treinado e é retirado uma parte dele, adicionado ao segundo modelo e colocado os novos itens para serem treinados, gerando as predições de acordo com o novo problema.

![[Pasted image 20250603172357.png]]

O reconhecimento de voz ou da fala é a tarefa de entender as palavras faladas de uma determinada pessoa. O reconhecimento automático da fala (_automatic Speech Recognition_ – ASR) refere-se à tarefa de reconhecer a fala humana e traduzi-la em texto. Esta área de pesquisa ganhou muito foco nas últimas décadas, muitas empresas utilizam este tipo de recursos, por exemplo, bancos, empresas de telefonia e empresas de telemarketing. O principal objetivo do ASR é através de um input de áudio transformar em uma sequência de palavras. Um sistema típico de ASR é formado por pré-processamento, extração de características, classificação e modelagem de linguagem. A Figura 2 (em inglês) ilustra o fluxo destes processos.

![[Pasted image 20250603172424.png]]

A etapa de pré-processamento visa melhorar o sinal de áudio reduzindo a relação sinal-ruído e filtrando o sinal, deixando com mais qualidade para ser processado posteriormente.

As características de ASR são extraídas com um número específico de valores ou coeficientes, que são gerados pela aplicação de vários métodos de entrada. Esta etapa deve ser robusta, considerando vários fatores de qualidade, como ruído e efeito de eco. A maioria dos métodos de ASR adota as seguintes técnicas de extração de características: _Mel-frequency cepstral coefficients_ (MFCCs) e _Discrete Wavelet Transform_ (DWT).

O modelo de classificação tem como objetivo achar o texto falado que está contido no sinal de entrada (voz). Ele utiliza os recursos extraídos da etapa anterior e gera o texto de saída.

Por fim, o modelo de linguagem é de grande importância, pois coloca o texto de acordo com as regras gramaticais e semânticas de uma língua. Os modelos reconhecem os tokens de saída do modelo de classificação e também fazem correções no texto de saída.

As redes neurais recorrentes (RNNs) são ideais para criar ASRs, pois executam cálculos considerando a sequência de dados temporais, ou seja, o estado atual, será dependente dos estados anteriores.

**Como aplicar na prática o que aprendeu**

Para aplicar na prática o conteúdo aprendido, o ideal é implementar uma deep net com transfer learning. No link a seguir vocês podem ver o passo a passo de uma aplicação desse tipo.

Disponível em: [https://medium.com/ensina-ai/transfer-learning-com-tensorflow-mais-f%C3%A1cil-do-que-voc%C3%AA-imagina-75c687fbf7be](https://medium.com/ensina-ai/transfer-learning-com-tensorflow-mais-f%C3%A1cil-do-que-voc%C3%AA-imagina-75c687fbf7be) **(Acesso em 10/01/2023)**

**Tópicos avançados**

O reconhecimento de voz é um assunto bastante amplo. O Python oferece uma biblioteca completa para implementação e é possível fazer vários testes com ela. Então, é recomendável utilizá-la. Disponível em: ([https://pypi.org/project/SpeechRecognition/](https://pypi.org/project/SpeechRecognition/)) . **(Acesso em 15/12/2022)**