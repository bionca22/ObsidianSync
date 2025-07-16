Podemos definir redes como _sistemas complexos_ compostos por **objetos** e **relacionamentos** entre esses objetos. Muito do que observamos à nossa volta pode ser representado dessa forma: redes formadas por **pessoas** (objetos) e **amizades** (relacionamentos); **aeroportos** (objetos) e **voos** (relacionamentos); **dispositivos de Internet** (objetos) e **conexões** (relacionamentos).

Podemos descrever uma rede matematicamente usando os conceitos de _Teoria dos_ Grafos. Dizemos que uma rede é um grafo composto por dois conjuntos **_V_** e **_E_**. O conjunto **_V_** é formado pelos **vértices**, também chamados de **nós**. Esses são os objetos que compõem a rede. Já o conjunto **_E_** contém as **arestas**, que relacionam pares de vértices na rede. A cardinalidade (número de elementos) do conjunto **_V_** indica o número de nós **_N_**. E a cardinalidade do conjunto **_E_** indica o número de arestas na rede, denotado por **_L_**.

Frequentemente, enumeramos os nós da rede usando um rótulo **_i = 0, 1,..., N – 1_**. Como não há uma ordem intrínseca entre os elementos do conjunto **_V_**, a escolha dos rótulos pode ser feita, em geral, de modo arbitrário. A partir dos rótulos dos nós no conjunto **_V_**, vamos identificar as arestas como pares **_(i, j)_** indicando a ligação entre os nós **_i_** e **_j_**. Por exemplo, a aresta _(1, 4)_ indica que há na rede uma relação entre os nós _1_ e _4_.

Numa rede **não direcionada**, temos **_(i, j)_** equivalente a **_(j, i)_**, ou seja, a relação entre dois nós será sempre bidirecional. Uma ligação entre os nós _1_ e _4_ pode ser denotada indistintamente por _(1, 4)_ ou _(4, 1)_. Por outro lado, em redes **direcionadas** temos **_(i, j)_** diferente de **_(j, i)_**. Em outras palavras, uma aresta _(1, 4)_ pode existir sem que a relação _(4, 1)_ esteja presente.

Em redes **com pesos**, cada uma das _L_ arestas possui como atributo um número real que indica o **custo** ou **distância** associado àquela relação entre dois nós. Por exemplo, uma aresta _(1, 4, 5.5)_ pode indicar que há uma ligação entre as estações de trem _1_ e _4_ e que a distância entre elas é de 5,5 km. O peso das arestas será fundamental no cálculo da **distância** entre dois nós. Em redes **sem pesos**, podemos assumir que todas as arestas possuem peso unitário, equivalente a “um salto” de um nó para outro.

Por fim, definimos como redes **com rótulos** aquelas cujos nós e/ou arestas possuem características (_features_) adicionais que diferenciam seus elementos. Por exemplo: se cada nó representa uma pessoa, podemos ter características como nome, idade e renda.

Usando nossa notação, teremos:
![[Pasted image 20250605093650.png]]

Cada um dos N nós de uma rede terá um grau, definido como o número de arestas ligadas a ele. Um nó sem arestas terá grau igual a zero.  
Dependendo do seu número arestas L, uma rede pode ser mais ou menos densa. Definimos a densidade de uma rede como a fração de arestas que existem na rede em relação ao maior número possível de arestas que poderia existir. Numa rede não direcionada, a densidade será dada pela equação 2LN(N−1)N(N−1)2L​ Em uma rede direcionada, a densidade será LN(N−1)N(N−1)L​

A densidade terá o valor mínimo 0 quando não houver arestas na rede e terá o valor máximo 1 quando houver arestas entre todos os pares de nós.

Definimos um **caminho** entre dois nós _i_ e _j_ em uma rede como uma sequência de nós **vizinhos** (ligados por uma aresta) que começa em _i_ e termina em _j_. Por exemplo: o caminho _[0, 5, 1]_ começa no nó _0_ e termina no nó _1_, passando pelas arestas _(0, 5)_ e _(5, 1)_. O **comprimento** de um caminho será dado pela soma do peso das arestas percorridas, assumindo que cada aresta em uma rede sem pesos possui peso 1. O caminho _[0, 5, 1]_, portanto, possui comprimento 2 se a rede não tem pesos.

O caminho mais curto entre dois nós _i_ e _j_ (aquele que possui menor comprimento) vai determinar a **distância** entre _i_ e _j_. Numa rede sem pesos, a distância será o número mínimo… de passos para ir de _i_ até _j_. Analisando a distância entre todos os pares de nós de uma rede, podemos calcular a **distância média** e a distância máxima, que é conhecida como **diâmetro** da rede**.** Dado um nó específico _i_, podemos também calcular sua **excentricidade** como a distância até o nó mais afastado de _i_.

Após nossas definições matemáticas, vamos ver como podemos iniciar nossa análise na prática usando a biblioteca _NetworkX_. O material completo está disponível nos _notebooks_ em nosso repositório. A instalação da biblioteca segue o processo padrão do _Python_. Basta executar pip install networkx.

Podemos criar uma rede (grafo) e adicionar nós e arestas da seguinte forma:

![[Pasted image 20250609093243.png]]

Se for uma rede **direcionada**, basta trocar **nx.Graph()** por **nx.DiGraph()**. Alternativamente, se quisermos ler a rede de um arquivo com **uma** **linha por aresta** podemos usar a função **nx.read_edgelist(CAMINHO_DO_ARQUIVO)**. Por exemplo, uma linha “4 2” no arquivo indica que os nós _4_ e _2_ devem ser inseridos juntamente com a aresta _(4, 2)_. Se nosso arquivo estiver em formato de **lista de adjacências**, podemos usar as funções **nx.read_adjlist** e **nx.read_multiline_adjlist**.

Após criar uma rede e armazenar numa variável **G**, podemos visualizá-la usando a função **nx.draw_networkx(G)**. Essa função aceita diversos parâmetros que permitem customizar o gráfico, como **font_weight** (para usar uma fonte em negrito) e **node_color** (para trocar a cor dos nós).

**Tópicos avançados**

Para aprender mais formas de visualizar redes usando o _NetworkX:_

- [https://networkx.org/documentation/stable/reference/drawing.html](https://networkx.org/documentation/stable/reference/drawing.html)

Para se aprofundar em _Teoria dos Grafos_ e conhecer a origem do estudo das redes, ler as Seções 2.1 e 2.2 do Capítulo 2 do livro do Barabási, disponível em:

- [http://networksciencebook.com/chapter/2#bridges](http://networksciencebook.com/chapter/2#bridges)