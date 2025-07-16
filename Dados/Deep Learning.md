Os algoritmos e funções de Deep Learning têm uma carga matemática bastante elevada. Neste material essa carga será minimizada, porém serão indicados materiais extras para recuperar este conteúdo.

Para começar a trabalhar com Deep Learning (DL) é importante conhecer quais são as principais representações (em outros materiais pode ser chamada de arquitetura) utilizadas para criar modelos. DL é uma subárea de Redes Neurais Artificiais (RNAs) e na Figura 1 (em inglês) são mostradas as principais representações de RNAs.

![[redes_neurais.png]]

É importante deixar claro o que caracteriza o Deep Learning em relação às RNAs: o DL é basicamente a utilização de uma ou várias camadas ocultas (_hidden cells_) em RNAs.

Hoje, iremos focar nas seguintes representações: Rede Neural Convolucional (Deep Convolutional Network – DCN ou Convolutional Neural Network - CNN), Rede Neural Recorrente (Recurrent Neural Network – RNN), Deep Belief Network (DBN) e Generative Adversarial Network (GAN). Algumas outras representações serão apenas comentadas de forma mais geral.

Não há uma representação generalista que possa ser considerada a melhor em relação a todas as outras. Cada representação tem seu conjunto de vantagens e desvantagens, além das aplicações a quais elas apresentam resultados eficientes. Sempre a escolha relacionada ao tipo de representação deverá levar em consideração diversos fatores, como: tipo de problema, tipo de dados de entrada, hardware disponível, ferramenta disponível, etc.


**Rede Neural Convolucional (CNN)**

CNN é uma representação de deep learning composta por múltiplas camadas ocultas totalmente conectadas com funções diferentes e geralmente aplicada para o **reconhecimento de imagens**. As camadas podem ser divididas em camada convolucional, camada de pooling e camada totalmente conectada.

A **camada convolucional** tem o papel de extrair os principais recursos dos dados de entrada e repassá-los para a próxima camada em forma de mapa de recursos. A **camada de pooling** é a responsável por reduzir a dimensionalidade dos dados aplicando camadas de agrupamento (pooling), fazendo com que o tempo de treinamento seja reduzido. Essa camada recebe cada saída da camada convolucional e prepara um mapa de características condensadas. A **camada totalmente conectada** é a responsável por realizar a tarefa de classificação. As pontuações de probabilidade são calculadas para cada possibilidade de classe por uma função de ativação popularmente chamada de função softmax.

As CNNs ajudam a suprir o problema de adequar o valor dos pesos de cada atributo de forma automatizada no seu processo de treinamento. Isso reduz o trabalho manual de modelar esses valores inicialmente.

**Rede Neural Recorrente (RNN)**

RNN são um tipo de RNA projetada para reconhecer dados de forma sequencial, como texto, fala, séries temporais, genomas, ações, entre outros. Esse tipo de arquitetura considera os dados em conjunto de tempo e sequência. Uma RNN mantém a memória interna através de um feedback e, assim, dá suporte ao comportamento temporal. O principal problema é que depois de um tempo as informações mais antigas acabam não fazendo sentido no contexto de momento.

Normalmente, as RNNs são compostas por três tipos de camadas: camada de entrada, camada intermediária ou oculta, e camada de saída. Cada neurônio da **camada de entrada** é conectado com cada neurônio da **camada oculta** seguinte, até a **camada de saída**, é comum os modelos terem mais de uma **camada oculta**.

As RNNs oferecem uma ideia geral e existem algoritmos mais específicos para sua aplicação, como: _Long_ / _Short Term Memory_ (LSTM) e o _Gated Recurrent Unit_ (GRU).

**Deep Belief Networks (DBN)**

DBNs são compostas por um conjunto de pequenas RNAs não supervisionadas. Uma das características comuns das DBNs é que, embora as camadas tenham conexões entre si, a rede não inclui conexões entre neurônios em uma única camada. Esta arquitetura pode gerenciar muitos dados devido a sua robustez e ao uso de camadas ocultas que reúnem correlações úteis dos dados e podem lidar com uma ampla variedade de tipos de dados. Como desvantagem, as DBNs requerem muitos dados de treinamento para obter um desempenho aceitável, fazendo com que seu treinamento se torne bastante caro.

As DBNs podem ser aplicadas para diversas tarefas supervisionadas e não supervisionadas, como: reconhecimento de imagens, reconhecimento de voz, sequência de vídeos, detecção de objetos, entre outros.

**Generative Adversarial Network (GAN)**

As GANs, diferentemente das arquiteturas apresentadas até agora, geram modelos generativos, as outras arquiteturas geram modelos discriminativos, ou seja, os modelos de GANs não visam fazer reconhecimento ou classificação de um conjunto de dados, mas sim a partir de um contexto, gerar dados com distribuições semelhantes ao que foi dado como entrada. Ela trabalha com duas redes que são colocadas uma contra a outra.

Uma rede é chamada de discriminadora, pois recebe os dados de entrada reais para ser treinada. Já a outra rede é chamada de rede geradora, porque recebe os dados de entrada com uma função de ruído e geram novos dados. Esses novos dados são enviados pelo modelo gerado pela rede discriminadora e ela avalia se são similares a alguma classe dos dados reais ou não. Caso não seja, o erro é propagado para a entrada da rede geradora para que gere outros dados, até que em dado momento haja uma convergência, onde a rede discriminadora não consiga mais detectar que os dados vindos da rede geradora sejam dados falsos.

As aplicações de GANs são inúmeras, como: melhoria de qualidade de imagens e vídeos e geração de dados para base de dados. Porém, também permite a possibilidade da geração de conteúdo fake com mais facilidade, pois seu desenvolvimento em termos de segurança ainda está em evolução.

**Tópicos avançados**

O conteúdo de deep learning tem uma carga matemática bastante pesada. Para se aprofundar nesse conteúdo, indica-se a visita nas referências bibliográficas, onde cada um destes algoritmos é apresentado de forma completa. Mais especificamente os capítulos 10, 40, 48 e 54.

Deep Learning Book. **Data Science Academy**, 2022. Disponível em: <[https://www.deeplearningbook.com.br/](https://www.deeplearningbook.com.br/) >. **(Acesso em 15/12/2022).**

---

## Parâmetros de Ajuste Usando Retropropagação.

Um dos principais problemas das Redes Neurais Artificiais (RNAs) é a definição dos parâmetros de treinamento dos modelos, definição do peso dos atributos de entrada, da taxa de aprendizado, do número de neurônios, quantidade de camadas, entre outros. Estas definições acabam tomando bastante tempo e devem ser testadas diversas configurações até que seja encontrada uma configuração eficiente para o problema. Os algoritmos de treinamento estáticos não alteravam estes valores e nem a estrutura da rede. Para uma modificação, era necessário começar todo o treinamento novamente. Com isso, surgiram os algoritmos dinâmicos, que podem alterar a estrutura da rede, isto é, podem alterar a quantidade de camadas, o número de neurônios das camadas intermediárias e também as interligações na rede. O método dinâmico que se destaca é o backpropagation ou de retropropagação.

A otimização do backpropagation é dada pelo gradiente descendente, onde os pesos são ajustados para reduzir o erro da rede. Durante o treinamento, os padrões de entrada são dados como entrada para a RNA em uma determinada ordem. Cada um desses padrões é propagado para frente na rede, até a camada de saída, a saída computada pela rede é comparada com a saída esperada, esta comparação irá gerar um valor que dirá o erro (fase _forward_). Este erro será utilizado para realimentar as conexões e fazer o ajuste dos pesos de cada camada no sentido oposto. Dessa forma, os erros farão diversos ajustes nos pesos para se aproximar das saídas que são esperadas, e isso vai fazer que neurônios que foram ativados em um momento, possam não ser ativados em outro momento (fase _backward_). Todo o processo é feito novamente até que uma condição de parada seja satisfeita (número de interações, convergência do resultado, etc.).

A Figura 1 (em inglês) demonstra uma representação do processo de treinamento do algoritmo backpropagation, onde o Forwardpass é a fase forward e o Backwardpass é a fase backaward.

![[Pasted image 20250531131417.png]]

Quando pensamos em utilizar as RNAs, fica predeterminado que é necessário definir um conjunto de parâmetros. Agora, serão apresentados alguns deles. O algoritmo backpropagation auxilia o treinamento do modelo depois que os parâmetros iniciais já foram definidos.

O número de camadas ocultas ou intermediárias influencia o erro médio do modelo, então a escolha da quantidade depende bastante do tipo de arquitetura que está sendo utilizada, evidentemente que se for uma arquitetura de Deep Learning (DL) por padrão já será utilizada inúmeras camadas deste tipo.

O número de neurônios na camada oculta deve ser decidido de forma bastante criteriosa, pois um número muito alto pode gerar um _overfitting_ (superajuste dos dados) e um número muito baixo pode gastar muito tempo para encontrar uma convergência no treinamento. Existem propostas para definição da quantidade destes neurônios em função do número de camadas de entrada e saída da rede.

A Taxa de aprendizado varia de 0.1 a 1.0 e tem grande influência durante o processo de treinamento da RNA. Uma taxa muito baixa faz com que o aprendizado seja muito lento, ao passo que uma taxa muito alta provoca oscilações no treinamento e impede a convergência neste processo de aprendizado.

**Padrão por Ciclos**

Vamos agora falar sobre a dinâmica de treinamento por padrão e por ciclo. Na dinâmica por padrão, após a apresentação de cada exemplo de treinamento, os pesos são ajustados, pois a ordem dos padrões é importante para a velocidade de aprendizado da rede e, em alguns casos, deve-se reorganizar esta ordem, de forma a acelerar o treinamento. Geralmente, o treinamento desta abordagem é mais rápido, porém pode se tornar instável. Na dinâmica por ciclo, após a apresentação de todos os exemplos, os pesos são ajustados, pois o treinamento desta abordagem costuma consumir mais memória e o tempo de treinamento é mais lento, porém é mais estável.

Por fim, um outro parâmetro importante é o critério de parada do treinamento, podendo ser: número de ciclos, erro, combinação dos métodos anteriores e validação. O número de ciclos define quantos ciclos serão passados pela rede, ou seja, o número de vezes que aquele conjunto de exemplos será apresentado na rede e terá todo seu processamento feito e atualizado. O erro consiste em encerrar o treinamento após o erro médio quadrático ficar abaixo de um valor predefinido. A combinação dos métodos anteriores é quando qualquer um dos dois critérios anteriores forem alcançados. E o critério de validação ocorre onde o treinamento é parado a cada número determinado de ciclos e é realizada uma estimação do erro da rede sobre o conjunto de dados de teste. No momento em que o erro medido no conjunto de teste apresentar crescimento, o treinamento é encerrado para encontrar o momento onde a rede perdeu o poder de generalização dela.

Definir todo esse conjunto de parâmetros não é uma tarefa fácil, mas algumas arquiteturas nos ajudam na escolha de algum deles. A implementação prática do backpropagation e todas essas escolhas serão feitas nas videoaulas.

**Como aplicar na prática o que aprendeu**

Implementar o algoritmo backpropagation junto a alguma arquitetura de RNA (Implementação em Python – Capítulo 16 da referência).

**Tópicos avançados**

O algoritmo backpropagation tem uma carga pesada de matemática, principalmente com o uso de derivadas. Para o entendimento dos cálculos complexos dele, sugiro que faça a leitura dos capítulos da referência: 14, 15 e 16.

Deep Learning Book. **Data Science Academy**, 2022. Disponível em: <[https://www.deeplearningbook.com.br/](https://www.deeplearningbook.com.br/) >. **(Acesso em 15/12/2022).**

----
# Funções Não Convexas

**Resumo**

As funções convexas e não convexas estão dentro do tema de otimização que é uma área multidisciplinar que inclui inteligência artificial, matemática, pesquisa operacional, logística, entre diversas outras áreas. Para a maioria dos problemas, as funções convexas ofereciam soluções satisfatórias e em poucos casos usavam-se as funções não convexas. Com o surgimento do Deep Learning (DL), os problemas solucionáveis através dos algoritmos de DL começaram a oferecer situações onde as funções não convexas se tornam necessárias para trazer maiores benefícios. A Figura 1 ilustra os gráficos de uma função convexa sendo representada à esquerda pela cor azul e de uma função não convexa e à direita na cor vermelha.

![[Pasted image 20250531144305.png]]

De forma bem superficial, as funções convexas são definidas como um subcampo da otimização matemática que lida com a minimização sobre conjuntos convexos. Elas são interessantes, pois em muitos casos o tempo de convergência é polinomial. Programação Linear (PL) e problema de mínimos quadrados são casos especiais de otimização convexa. Se um problema puder ser formulado como um problema de otimização convexa, então este problema poderá ser resolvido com eficiência, pois muitos métodos eficazes estão disponíveis na literatura.

No caso das funções não convexas, elas tratam qualquer problema em que o objetivo ou qualquer uma das restrições não são convexas. Nesse caso, mesmo problemas aparentemente simples com apenas dez variáveis podem ser desafiadores, enquanto problemas com algumas centenas de variáveis já se tornam praticamente intratáveis. Com isso, foram criados algoritmos que são capazes de fazer concessões para que se possa alcançar resultados factíveis e ainda assim interessantes, mesmo que não sejam ótimos. Estes algoritmos abrem possibilidades para a busca local, onde encontrar um bom ponto que pode ser suficientemente eficiente.

Encontrar um resultado ótimo com a otimização não convexa se torna problemático por diversos fatores, entre eles: ter várias regiões factíveis e muito planas, uma curvatura amplamente variável, vários pontos de montagem e vários mínimos locais dentro de cada região. Pode levar um tempo exponencial no número de variáveis e restrições para determinar a inviabilidade de solução de um problema desse tipo.

As redes neurais por padrão são aproximadores de funções universais, com neurônios suficientes que têm a capacidade de aproximar bem qualquer tipo de função. Dentre as funções a serem aproximadas, as funções não convexas estão ganhando mais destaque principalmente com o uso de DL. Na otimização não convexa, muitas funções convexas podem ser utilizadas, como _stochastic gradient_ descent (SGD), _mini-batching_, _stochastic variance-reduced gradient_, e _momentum_. Existem também métodos especializados para resolver problemas não convexos conhecidos na pesquisa operacional, como método de minimização alternada, método _branch-and-bound_. Contudo, geralmente, esses métodos não são tão populares para problemas de aprendizado de máquina.

---
# Manipulação de Deep Nets

**Resumo**

As Deep Nets ou Redes Profundas precisam de parâmetros e hiperparâmetros para iniciar o processo de treinamento. Os parâmetros são os coeficientes (pesos iniciais dos atributos de entrada) dos modelos e são escolhidos pelos próprios modelos para minimizar o erro, o único papel manual é iniciar o valor deles. Já os hiperparâmetros, precisam ser configurados manualmente e não serão atualizados de forma automática. Dentre os hiperparâmetros estão o número de camadas ocultas, a taxa de aprendizado, momentum, função de ativação e critério de parada.

O número de camadas ocultas vai ser definido junto à arquitetura escolhida e ao número de neurônios na camada de entrada e na camada de saída. A taxa de aprendizado vai ser um valor entre 0.1 e 1.0 e vai definir o quão rápido vai ser a convergência do aprendizado, sendo que uma taxa muito alta faz com que ele não tenha tanto tempo para conseguir aprender de forma eficiente e uma taxa muito baixa faz com que o tempo de treinamento seja muito alto. O momentum, basicamente, aumenta a velocidade de convergência do treinamento em termos de manter uma memória de uma direção anterior que era correta. Existem diversas funções de ativação. São funções que definem se os neurônios serão ou não ativados, algumas das mais conhecidas e utilizadas são a ReLU, sigmóide e Softmax. Os critérios de parada são as definições para o algoritmo para o treinamento, o principal é o número de épocas predefinidas.

Há diversas funções de ativação para as Deep Nets, porém aqui serão apresentadas as funções _sigmóide_, _ReLU_ e _Softmax_.

A função sigmóide tem uma natureza não linear na sua formação no plano cartesiano, ou seja, ela não trabalha somente com 0 ou 1. Ela é especialmente usada quando queremos utilizar modelos para prever uma probabilidade de saída. Geralmente, esta função é utilizada na camada de saída devido a sua alta carga de cálculo de derivadas e exponencial. A figura 1 representa a curva da função sigmóide. A fórmula a seguir é utilizada para o cálculo da função:

![[Pasted image 20250602192137.png]]

A função Linear Retificada (_Rectified Linear Unit_ – ReLU) é utilizada para permitir o treinamento de redes neurais profundas supervisionadas sem a necessidade de pré-treinamento não supervisionado. Sobre a função sigmóide, a função ReLU, permite um treinamento mais rápido e efetivo das arquiteturas de Deep Nets em conjuntos de dados grandes e complexos, pois não utiliza cálculo de expoentes, ela realiza apenas operações de comparação, adição e multiplicação. Esta função é definida através da parte positiva do seu argumento, ou seja, sempre que houver valores negativos na sua entrada, esse valor será zerado e o neurônio não será ativado. Dessa forma, apenas alguns neurônios serão ativados, deixando a rede neural esparsa. Geralmente é utilizada nas camadas profundas. A figura 2 representa a curva da função ReLU. A fórmula a seguir é utilizada para o cálculo da função:


![[Pasted image 20250602192207.png]]


A função softmax é usada para a classificação multiclasse. Ela calcula a distribuição de probabilidades do evento nos diferentes rótulos possíveis totalizando a somatória 1. As probabilidades calculadas auxiliam na determinação da classe final para os valores de entrada fornecidos e também é bastante utilizada na camada de saída. A figura 3 representa a curva da função softmax. O cálculo da função é dado por:

![[Pasted image 20250602192235.png]]

Não existe a melhor função de ativação, a função sempre vai depender do problema, da arquitetura e do tipo de treinamento que deseja ser realizado. A mudança das funções pode resultar em mudanças significativas nos resultados.

As Deep Nets podem ser treinadas de diversas formas. Três delas são as mais comuns e serão explicadas neste módulo. São elas: treinamento do zero, treinamento por transferência (_transfer learning_) e extração de recursos.

O treinamento do zero requer um conjunto de dados rotulados robusto e a projeção de uma arquitetura que irá aprender os recursos e o modelo será gerado a partir disso. Isso é bom para novas aplicações ou para aplicações que tem um número elevado de classes de saída. Essa é uma abordagem menos comum, pois com a grande quantidade de dados necessários e a taxa de aprendizado, essas redes geralmente levam muito tempo para serem treinadas, podendo levar dias ou até mesmo semanas.

O treinamento por transferência é utilizado pela maior parte das aplicações de Deep Nets. É um processo que envolve o ajuste fino de um modelo pré-treinado. O processo usa uma rede existente e já treinada, como o GoogLeNet, e é alimentada com novos dados contendo novas classes anteriormente desconhecidas. Depois de fazer alguns ajustes na rede, ela fica adaptada para realizar uma nova tarefa, como categorizar leão e tigre em vez de 1000 objetos diferentes. Com isso, tem também a vantagem de precisar de muito menos dados (processando milhares de dados, ao invés de milhões) de modo que o tempo de computação diminui para minutos ou horas. Este tipo de treinamento será explorado mais detalhadamente em outro módulo deste curso.

O processo de extração de recursos em Deep Nets é um pouco menos comum e mais especializado, usando a rede como extrator de recursos. Como todas as camadas têm a tarefa de aprender certos recursos dos dados, podemos extrair esses recursos da rede a qualquer momento durante o processo de treinamento. Estes recursos podem ser usados como entrada para um modelo de aprendizado de máquina tradicional.

**Tópicos avançados**

Conhecer as arquiteturas, os parâmetros e os hiperparâmetros é extremamente importante para o sucesso dos modelos de Deep Nets. Para isso, sugiro que faça a leitura do capítulo 26 do livro “Deep Learning Book”.

----
## Processamento de Linguagem Natural

O Processamento de Linguagem Natural (PLN) trabalha com o desenvolvimento de modelos computacionais que dependem da linguagem humana. Esta técnica trabalha com dados não estruturados de texto e seu domínio costuma ser bem difícil, porém sua ideia e seus conceitos são fáceis de entender.

A PLN pode ser aplicada para diversos problemas: classificação de produtos, análise de sentimentos, resumo de texto, tradução, fala em texto e geração de texto. As principais vantagens de se usar PLN são fazer análises em larga escala, obter uma análise mais objetiva e precisa, simplificar processos e reduzir custos, melhorar a satisfação de clientes, entender melhor o seu mercado e o comportamento dos clientes, capacitar seus funcionários e obter insights reais e acionáveis.

A ideia é a partir de um conteúdo textual extrair algum tipo de conhecimento para gerar uma das vantagens citadas anteriormente. Contudo, para que isso ocorra é necessário levar em consideração toda a análise do teor do texto em nível de contextualização, semântica, situação, entre outras coisas, e aí que está a parte difícil de passar para os modelos computacionais. Existem várias técnicas que possibilitam que o processamento do texto tenha informações mais concisas com o pensamento de um humano lendo ele. Algumas técnicas serão apresentadas a seguir.

A técnica de _tokenização_ é quando cada palavra é separada em pequenas partes (chamadas de tokens). Os tokens são fundamentais para que o software determine quais palavras estão realmente presentes no texto e conceda uma identificação para cada uma delas.

Sobre as técnicas de stemização e lematização, os dois processos são semelhantes e têm como resultado a simplificação de palavras como “andando” para apenas “andar”. Essa prática torna o processamento mais ágil e simples para os modelos de Inteligência Artificial.

A técnica _n-grams_ é um modelo para simplificar o conteúdo da seleção de texto. Considerando a ordem do conjunto de palavras, a modelagem de n-gramas está interessada em preservar sequências contíguas de N itens da seleção de texto.

A técnica _stop-words_ é utilizada para remover palavras que não agregam muito valor a uma frase, como “a”, “ainda”, “algo”. Com isso, é possível economizar recursos na hora do processo de treinamento.

A técnica _bag of words_ cria um vetor com as palavras contidas no texto e sua quantificação. As palavras podem ser vistas independentemente e sua frequência pode identificar a sua significância para o contexto da situação.

Essas são algumas das técnicas que podem ser aplicadas para que os textos sejam pré-processados e treinados em um determinado modelo inteligente. A Figura 1 ilustra os passos de criação de um sistema de PLN.

![[Pasted image 20250604192436.png]]

Como já falamos anteriormente, as tarefas de PLN são inúmeras. Agora, vamos falar mais especificamente de algumas delas.

A Tarefa de tradução de idiomas é uma tarefa tradicional da PLN e vem sendo estudada faz bastante tempo. Ela consiste na passagem de um texto de um idioma para outro. Antigamente os tradutores virtuais não conseguiam fazer uma tradução muito efetiva, geralmente a tradução era feita palavra por palavra, sem considerar o contexto. Hoje, para alguns idiomas melhorou bastante com a adição de contexto, porém alguns ainda têm padrões que são bem difíceis de serem percebidos e utilizados para automatizar os tradutores. Mesmo com as melhorias, quando há textos muito complexos os tradutores ainda têm uma certa dificuldade para conseguir fazer a tradução efetiva.

Outra tarefa bastante tradicional de PLN é o filtro de e-mail, que consiste no reconhecimento de spam. A leitura do texto junto ao cruzamento de outros dados, como remetente, ajuda no reconhecimento deste tipo de e-mail. Além disso, o Gmail também já detecta e-mails relacionados às redes sociais e também promocionais, separando-os dos principais. Nessa tarefa ainda há espaço para a expansão, no sentido de criar mecanismos ainda mais robustos de caracterização de e-mails em diversos outros subníveis.

Na tarefa de resultados de pesquisa são mostrados resultados com base em pesquisas semelhantes ou na intenção do usuário. Nem sempre precisamos saber um termo exato de pesquisa, mas com um termo aproximado conseguimos achar o que desejamos. É bem comum alguém ouvir falar sobre uma música ou um cantor e não saber exatamente como escreve o nome, mas junta o conjunto de informações e a busca se torna efetiva e acaba encontrando o que deseja. Cada vez mais os dispositivos de pesquisa buscam melhorar seus sistemas, se tornando mais eficientes e abrangentes para que os usuários realmente encontrem o que estão procurando, não só no google, mas também nos aplicativos de áudio, vídeo, entre outros.

Os assistentes virtuais inteligentes começaram a se popularizar e também são um exemplo de uso da PLN, pois capturam a voz do usuário, fazem o processamento dela e uma pesquisa de acordo com o que foi solicitado. A Siri e a Alexa são as mais famosas nesse quesito e são bastante eficientes. Várias informações podem ser processadas e vários tipos de respostas podem ser coletadas dessas assistentes. O conjunto de recursos tem a tendência de sempre aumentar e a conectividade com outros aplicativos e aparelhos domésticos também.

Existem várias outras tarefas de PLN. Nas videoaulas iremos implementar uma destas tarefas passo a passo.

**Tópicos avançados**

Algumas arquiteturas de PLN foram criadas baseadas no Deep Learning, como Transformer, Bidirectional Encoder Representations From Transformers (BERT) e Generative Pré-Trained Transformer (GPT). Para ter mais conhecimento sobre as arquiteturas, recomendo as seguintes leituras: Transformer ([https://ieeexplore.ieee.org/abstract/document/9038381](https://ieeexplore.ieee.org/abstract/document/9038381)), BERT ([http://primo.ai/index.php?title=Bidirectional_Encoder_Representations_from_Transformers_(BERT)](http://primo.ai/index.php?title=Bidirectional_Encoder_Representations_from_Transformers_\(BERT\))) e GPT ([http://primo.ai/index.php?](http://primo.ai/index.php?title=Generative_Pre-trained_Transformer_\(GPT\))[title=Generative_Pre-trained_Transformer_(GPT)](http://primo.ai/index.php?title=Generative_Pre-trained_Transformer_\(GPT\))) **(Acesso em 15/12/2022)**

---

## Cross-Entropy

**Resumo**

Para começarmos a falar da função cross-entropy ou entropia cruzada, precisamos primeiramente falar de entropia. A entropia é definida como o menor tamanho médio de codificação por transmissão com o qual uma origem pode enviar uma mensagem a um destino com eficiência sem perda de dados. Ela pode ser definida matematicamente utilizando uma distribuição de probabilidade denotada como H. Quando utilizamos variáveis categóricas, a fórmula é a seguinte:

![[Pasted image 20250604193512.png]]

Já na entropia cruzada, suponha que temos duas distribuições de dados e precisamos compará-las. A entropia cruzada emprega o conceito de entropia apresentado anteriormente. Ela é uma medida da diferença de entropia entre duas distribuições de probabilidade. Suponha que a primeira distribuição de probabilidade seja denotada por A e a segunda distribuição de probabilidade seja denotada por B. O número médio de bits necessários para enviar uma mensagem da distribuição A para a distribuição B é chamado de entropia cruzada. Este conceito é usado no aprendizado de máquina quando algoritmos são criados para prever a partir do modelo. A construção do modelo é baseada na comparação dos resultados reais e esperados. A Fórmula para calcular a entropia cruzada é a seguinte:

![[Pasted image 20250604193932.png]]

Na equação acima, x é o número total de valores e p(x) é a probabilidade de distribuição no mundo real. Na distribuição projetada B, A é a distribuição de probabilidade e q(x) é a probabilidade de distribuição. Então, trabalhando com duas distribuições, como ligamos a entropia cruzada com a entropia? Se os valores esperados e reais forem os mesmos, a entropia cruzada e a entropia são iguais. No mundo real, no entanto, o valor previsto difere do valor real que é referido como divergência, porque eles diferem ou divergem do valor real. Como resultado, a entropia cruzada é a soma da entropia e da divergência KL (tipo de divergência).

Ao otimizar modelos de classificação, a entropia cruzada é comumente empregada como uma função de perda (função de erro). A técnica de regressão logística e rede neural artificial podem ser utilizadas para problemas de classificação. Na classificação, cada caso tem um rótulo de classe conhecido com uma probabilidade de 1.0, enquanto todos os outros rótulos têm uma probabilidade de 0.0. O modelo calcula a probabilidade de um determinado exemplo pertencer a cada rótulo de classe. A diferença entre duas distribuições de probabilidade pode, então, ser calculada usando a entropia cruzada.

Na classificação, o objetivo da distribuição de probabilidade P para uma entrada de rótulos de classe 0 e 1 é interpretado na probabilidade como Impossível ou Certo. Como essa probabilidade não inclui surpresas (eventos de baixa probabilidade), eles não têm conteúdo de informação e têm entropia zero. Quando estamos lidando com a probabilidade de Duas Classes, a probabilidade é modelada como distribuição de _Bernoulli_ para a classe positiva. Isso significa que o modelo prevê explicitamente a probabilidade para a classe 1, enquanto a probabilidade para a classe 0 é dada como 1 – probabilidade projetada. Para ficar mais claro:

Classe 1 = 1 (originalmente previsto).

Classe 0 = 1 - originalmente previsto.

Estamos frequentemente preocupados em diminuir a entropia cruzada do modelo em todo o conjunto de dados de treinamento. Isso pode ser feito tomando a entropia cruzada média de todos os conjuntos de treinamento.

A demonstração do uso da função de entropia cruzada será feita na videoaula através da implementação e avaliação dos resultados obtidos a partir dela.

**Tópicos avançados**

O conteúdo mais específico sobre funções de ativação e cross-entropy é apresentado no livro “Deep Learning Book”, mais especificamente nos capítulos 17 e 18.

----

## Regressão Logística

A regressão logística (RL) é um algoritmo de classificação usado para atribuir observações a um conjunto discreto de classes. Alguns dos exemplos de problemas que podem ser aplicados são: classificação de e-mail, spam ou não, transações online fraudulentas ou não, tumores malignos ou benignos. A RL transforma sua saída utilizando a função sigmóide logística para retornar um valor de probabilidade. A RL pode fazer classificações do tipo binária ou multiclasses.

Antes de aplicarmos o algoritmo de RL, é importante cumprir a tarefa de pré-processamento que inclui diversos tratamentos dos dados que serão explicados a seguir:

**Remoção de ruídos e outliers**: a RL não consegue trabalhar com dados ruidosos ou fora dos padrões apresentados. Então, todos os dados de entrada devem ser conferidos e padronizados.

**Distribuição Gaussiana:** a regressão logística é um algoritmo linear (com uma transformação não linear na saída). Ele assume uma relação linear entre as variáveis de entrada com a saída. Transformações de dados de suas variáveis de entrada que expõem melhor essa relação linear podem resultar em um modelo mais preciso. Por exemplo, você pode usar log, root, Box-Cox e outras transformações univariadas para expor melhor esse relacionamento.

**Remover entradas correlacionadas, na regressão linear**: o modelo pode sofrer um _overfitting_, se existirem várias entradas altamente correlacionadas. Considere calcular as correlações pareadas entre todas as entradas e remover entradas altamente correlacionadas, para não cair no problema.

**Falha de convergência**: é possível que o processo de estimativa de verossimilhança esperada, que aprende os coeficientes, não tenha convergência. Isso pode acontecer se houver muitas entradas altamente correlacionadas em seus dados ou se os dados forem muito esparsos (por exemplo, muitos zeros em seus dados de entrada).

Todos os itens acima devem ser tratados. A partir daí, será aplicado o algoritmo de RL e gerado o modelo de classificação a partir dele.

Para o melhor entendimento da RL, vamos rever a função sigmóide. A figura 1 representa a curva da função sigmóide. A fórmula a seguir é utilizada para o cálculo da função:

![[Pasted image 20250604195836.png]]

A fórmula simplificada de cálculo da RL é denotada a seguir:

![[Pasted image 20250604195916.png]]

Estas fórmulas são utilizadas para gerar o modelo de RL. O algoritmo de RL pode ser utilizado junto com a função de ativação sigmóide em arquiteturas de Deep Learning para melhorar o desempenho de modelos criados.

Os algoritmos de classificação podem ser avaliados a partir de uma matriz de confusão que é gerada e do seu resultado final. A partir da matriz de confusão podem ser calculadas diversas métricas. A Figura 2 mostra uma matriz de confusão. É gerada com os eixos de linhas e colunas com todas as classes possíveis. Quando o valor de Y = 1 é igual ao valor de Ŷ = 1, significa que o valor original era 1 e o valor estimado pelo modelo também foi 1, então o VP significa Verdadeiro Positivo. Quando o valor de Y = 1 é igual ao valor de Ŷ = 0, significa que o valor original era 1 e o valor estimado pelo modelo foi 0, então o FN significa Falso Negativo, pois era para ser 1. Quando o valor de Y = 0 é igual ao valor de Ŷ = 1, significa que o valor original era 0 e o valor estimado pelo modelo foi 1, então o FP significa Falso Positivo, pois era para ser 0. Quando o valor de Y = 0 é igual ao valor de Ŷ = 0, significa que o valor original era 0 e o valor estimado pelo modelo também foi 0, então o VN significa Verdadeiro Negativo.

![[Pasted image 20250604200141.png]]

A partir da matriz de confusão, podemos avaliar o modelo através de diversas métricas, dentre elas, a precisão, sensibilidade e especificidade.

A precisão representa a proporção das predições corretas do modelo sobre o total de eventos possível e é denotada por:

![[Pasted image 20250604200229.png]]

Onde P representa o total de classes positivas (Y=1) e N o total de classes negativas (Y = 0).

A sensibilidade é a proporção de verdadeiros positivos, ou seja, a capacidade do modelo avaliar o evento como Ŷ = 1 (estimado), dado que ele é evento real Y = 1:

![[Pasted image 20250604200314.png]]

A especificidade é a proporção de verdadeiros negativos, ou seja, o poder de predição do modelo em avaliar como “não evento” Ŷ = 0 sendo que ele não é evento Y = 0:

![[Pasted image 20250604200351.png]]

Os valores coletados destas métricas ajudam a avaliar os modelos de classificação e saber se eles devem ser reconfigurados e retreinados ou se estão suficientemente satisfatórios.

A implementação de uma tarefa de Regressão Linear será apresentada na videoaula.

----
