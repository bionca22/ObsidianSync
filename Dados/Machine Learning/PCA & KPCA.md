
**Resumo**

A maldição da dimensionalidade se refere a um fenômeno observado em muitos algoritmos de machine learning. Basicamente diz que aumentar o número de dimensões (features, variáveis) de um modelo não significa necessariamente melhorar seu desempenho e que quanto maior for o número de dimensões, mais dados serão necessários para que o modelo tenha um bom desempenho.

Além disso, o que acontece muitas vezes é que existem variáveis que são muito parecidas umas com as outras, ou mesmo que não são muito relevantes no conjunto de dados, e apenas dificultam a performance do modelo de machine learning a ser treinado.

Por isso, muitas vezes utilizamos algoritmos de redução de dimensionalidade para que cheguemos a uma quantidade menor de variáveis, mas que sejam mais significativas para o modelo de machine learning a ser utilizado, além de gerar melhores resultados.

O PCA é um algoritmo de aprendizado não supervisionado. A sigla significa Principal Component Analysis, que significa análise de componentes principais em inglês. O objetivo do PCA é transformar as variáveis originais para novas variáveis, chamadas de componentes principais. Elas são projeções dos dados em espaços de dimensão menor.

![[Pasted image 20250515180233.png]]

A ideia do componente principal é que ele seja o arranjo que melhor representa a distribuição dos dados. Aqui, o melhor significa que o componente principal precisa ter a maior variância possível e ter a menor distância média dos dados.

![[Pasted image 20250515180405.png]]

Geralmente, escolhemos o valor de K entre 2 a 3 dimensões, para ser possível visualizar os dados graficamente. Entretanto, é importante observar o quanto da variância foi explicada com os componentes principais escolhidos.

Para dados muito linearmente relacionados, os primeiros componentes irão explicar grande parte da variância, e o PCA funcionará muito bem.


**Vantagens**

- Funciona muito bem quando existem muitas variáveis linearmente relacionadas.
- Possui muitas adaptações.
- É muito utilizado, então é comum de outras pessoas conhecerem.
- Alto poder de representação.
- É de rápida execução.

**Desvantagens**

- Nem sempre é fácil escolher o valor de K.
- Não considera classes de dados já rotulados.
- Não funciona bem quando existem mais variáveis do que observações (perda de informação).
- Não funciona bem quando os dados estão em escalas muito diferentes.
- Sensível aos outliers.

O KPCA é um algoritmo de aprendizado não supervisionado. A sigla significa Kernel Principal Component Analysis. Análise de componentes principais via kernel em inglês.

O objetivo do KPCA é transformar as variáveis originais para novas variáveis, chamadas de componentes principais. Elas são projeções dos dados em espaços de dimensão menor. Ou seja, é exatamente o mesmo objetivo do PCA. A grande diferença é que o PCA é apropriado para quando os dados possuem uma relação linear, enquanto o KPCA consegue funcionar bem para conjuntos de dados com relações não lineares.

![[Pasted image 20250515180718.png]]

Para resolver os casos não lineares, o KPCA utiliza funções (kernel) para transformar os dados em um espaço linear, para então achar os componentes principais, exatamente igual ao PCA. O espaço transformado é chamado de espaço das features.

![[Pasted image 20250515180749.png]]

**Vantagens**

- Funciona muito bem para dados não linearmente relacionados.
- Muito utilizado para redução de dimensionalidade em imagens.

**Desvantagens**

- Nem sempre é fácil escolher o valor de K;
- O resultado depende da escolha da função kernel.
- O custo computacional pode ser alto para um grande volume de dados.
- Não temos uma boa explicabilidade.