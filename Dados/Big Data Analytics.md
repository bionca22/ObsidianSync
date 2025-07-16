Para começarmos nosso resumo, precisamos compreender o que seria um Big Data e como estes estão envolvidos na aplicação de algoritmos de aprendizagem de máquina.

Big Data representa um problema, uma vez que há um grande volume de dados que necessita de processamento computacional para análise e armazenamento. Neste sentido, um Big Data possui 5v´s que o representa: **_volume, variedade, velocidade, veracidade e valor_**. Vejamos cada um destes a seguir.

**1. Volume:** Big Data está relacionado com grande volume de dados que são gerados a cada segundo. Entre estes tipos de dados tem-se dados de mensagens, redes sociais, até mesmo dados relacionados a vídeos. Logo, a junção destes dados acarretam vários desafios, inclusive de análise.

**2. Variedade:** na atualidade, os dados podem assumir diversas características, como dados estruturados, que podem ser colocados em tabelas, e dados não-estruturados, como é o caso de fotos, vídeos, sons, representando mais de 80% dos dados mundiais.

**3. Veracidade:** garantir que os dados e informações são verdadeiros é uma tarefa complexa. Em Big Data não é diferente. A grande quantidade de dados e sua variedade pode ser uma grande propagadora de dados falsos. Logo, a atenção a este ponto deve ser prioritária.

**4. Velocidade:** refere-se à velocidade na qual os dados são criados. Isso inclui mensagens de redes sociais virais em segundos; transações de cartão de crédito sendo feitas a qualquer momento, ou os milissegundos necessários para calcular o valor de compra e venda de ações. O Big Data serve para analisar os dados no momento em que são criados, sem a necessidade de armazená-los em bancos de dados.

**5. Valor:** É importante que os dados agreguem valor para qualquer onde estes dados estão associados. Não adianta ter uma grande quantidade de dados, se estes não contribuírem para robustas análises e tomada de decisões.

Para analisar esse grande volume de dados torna-se necessário obter ferramentas analíticas e frameworks, que podem ser chamadas de Big Data Analytics.

Quanto às ferramentas e frameworks existentes, o mais importante está associado a frameworks que consigam agregar e analisar dados, uma vez que um framework é uma estrutura geral que possui diversas ferramentas que permite a inclusão e análise de dados (considerando o cenário em que estamos trabalhando). Quando falamos do universo BIG DATA, um dos frameworks mais famosos para realizar diversas atividades é chamado de HADOOP.

A biblioteca Hadoop é um framework que de acordo com Apache, 2021:

permite o processamento distribuído de grandes conjuntos de dados por meio de clusters de computador usando modelos de programação. Ele foi projetado para garantir ampla escalabilidade de um único servidor a um cluster com milhares de máquinas, cada uma oferecendo computação local e capacidade de armazenamento. Em vez de depender de hardware para fornecer maior disponibilidade, a própria biblioteca foi projetada para detectar e resolver falhas na camada de aplicativo para fornecer um serviço de alta disponibilidade baseado em uma grade de computadores.

![[Pasted image 20250527213941.png]]

Nesta estrutura básica verifica-se algumas ferramentas que contribuem para a configuração e análise de grandes volumes de dados. Vamos entender cada uma delas. Neste momento falaremos das duas principais ferramentas envolvidas no processo de análise de grande volume de dados: Ambari e Hive

**AMBARI (Management)**

O ambari é uma central de gerenciamento do banco de dados. Nele é possível identificar nível de desempenho e processamento.

**HIVE (Query)**

O _Hive_ possibilita fazer consultas, modificar e apagar dados provenientes de grandes volumes de dados. Neste caso basta utilizar o padrão _query_ já é conhecido em outros sistemas de gerenciamento de banco de dados (SGBD).

Estas ferramentas contribuem para a análise e desempenho no processamento de dados em sistemas que possuem grandes volumes de dados. Com tudo isso, o que queremos é ter uma estruturação de dados mais eficiente e que possibilite contribuir para diversos processos existentes em organizações públicas e privadas e que permita análises em tempo real.

**Como aplicar na prática o que aprendeu**

Você sabia que Big Data Analytics tem ajudado na interpretação de informações em diversas áreas? Por exemplo, na segurança pública. Esta área possui uma enorme quantidade de dados em tempo real e a necessidade de entender como estão geograficamente distribuídos, correlacionar uma abordagem a diferentes textos que tenham o mesmo significado e extrair informações relevantes dentro de centenas ou milhares de texto é uma tarefa complicada que requer processamento em tempo real. Para dar conta da missão e obter resultados rápidos e eficientes, são necessárias unidades de inteligência, bem como equipamentos e programas de computador que utilizam tecnologias de Big Data para análise em tempo real.

**Tópicos avançados**

Um ponto importante a compreender nesse cenário é que os termos BIG DATA e BIG DATA ANALYTICS possuem significados diferentes. O primeiro está relacionado ao grande volume de dados existentes em banco de dados. Estes dados podem ser estruturados e podem ser não estruturados. Os dados estruturados são dados comuns, como nome, cpf e localidade. Já os dados não estruturados são dados mais complexos e envolvem imagens, textos e frases. Imagina quando todos estes dados estão unidos em repositórios? Daí chamamos de BIG DATA.

Por outro lado, quando temos ferramentas e frameworks que tem como finalidade analisar estes grandes volumes de dados estamos chamando de BIG DATA ANALYTICS. O termo ANALYTICS em sua tradução para o português será ANALITÍCO, ou seja, ferramentas analíticas tecnológicas que comportem esta análise (sejam tecnologias, modelos e matemática).

Para saber mais informações, acessar esse link:

KHAN ACADEMY. A era do Big Data. Disponível em: < [https://www.khanacademy.org/computing/ap-computer-science-principles/data-analysis-101/big-data/a/what-is-big-data](https://www.khanacademy.org/computing/ap-computer-science-principles/data-analysis-101/big-data/a/what-is-big-data)>. Acesso em: 30 de nov. 2022

Caro estudante, você consegue acessar os códigos utilizados na disciplina no link a seguir: [https://github.com/FaculdadeDescomplica/RegressaoePredicao](https://github.com/FaculdadeDescomplica/RegressaoePredicao)

---
## Regressões Lasso e Ridge

A regressão Ridge e Lasso são técnicas poderosas geralmente usadas para criar modelos que possuam um "grande" número de recursos. Aqui, ‘grande’ pode normalmente significar uma de duas coisas:

- Grande o suficiente para aumentar a tendência de um modelo de overfitting (tão baixo quanto 10 variáveis podem causar overfitting)
- Grande o suficiente para causar desafios computacionais. Com sistemas modernos, essa situação pode surgir no caso de milhões ou bilhões de recursos.

Embora Ridge e Lasso possam parecer trabalhar para um objetivo comum, as propriedades inerentes e os casos de uso prático diferem substancialmente. Se você já ouviu falar deles antes, deve saber que eles funcionam penalizando a magnitude dos coeficientes dos recursos, além de minimizar o erro entre as observações previstas e reais. Estas são chamadas de técnicas de “regularização”. A principal diferença está em como eles atribuem penalidade aos coeficientes:

**_Regressão Ridge:_**

A regressão ridge realiza ‘regularização L2’, ou seja, adiciona um fator de soma de quadrados de coeficientes no objetivo de otimização. Assim, a regressão otimiza o seguinte:

**Objetivo = RSS + α * (soma do quadrado dos coeficientes)**

Aqui, α (alfa) é o parâmetro que equilibra a quantidade de ênfase dada à minimização de RSS versus minimização da soma do quadrado dos coeficientes. α pode assumir vários valores:

**α = 0:**

O objetivo passa a ser o mesmo da regressão linear simples.

Obteremos os mesmos coeficientes da regressão linear simples.

**α = ∞:**

Os coeficientes são zero. Por quê? Por causa do peso infinito no quadrado dos coeficientes, qualquer coisa menor que zero tornará o objetivo infinito.

**0 < α < ∞:**

A magnitude de α decidirá o peso dado às diferentes partes da objetiva e os coeficientes estarão em algum lugar entre 0 e um para regressão linear simples.

Em Python se torna simples a inclusão de uma regressão Ridge através da biblioteca Sklearn (Figura 1):

![[Pasted image 20250529073815.png]]

**_Regressão de lasso:_**

A regressão Lasso realiza a regularização L1, ou seja, adiciona um fator de soma do valor absoluto dos coeficientes no objetivo de otimização. Assim, a regressão de laço otimiza o seguinte:

Objetivo = RSS + α * (soma do valor absoluto dos coeficientes)

Aqui, α (alfa) funciona de maneira semelhante à de ridge e fornece uma compensação entre o RSS de balanceamento e a magnitude dos coeficientes. Naturalmente, α pode assumir vários valores. Vamos descrevê-los aqui brevemente:

α = 0: Mesmos coeficientes da regressão linear simples

α = ∞: Todos os coeficientes zero (mesma lógica de antes)

0 < α < ∞: coeficientes entre 0 e o da regressão linear simples

Em Python se torna simples a inclusão de uma regressão Lasso através da biblioteca Sklearn (Figura 2):

![[Pasted image 20250529073932.png]]

Agora que temos uma boa ideia de como funcionam as regressões de ridge e lasso, vamos tentar consolidar nosso entendimento comparando-as e apreciar seus casos de uso específicos.

Quanto a diferença, a Ridge inclui todas (ou nenhuma) características do modelo. Assim, a principal vantagem da regressão do ridge é o encolhimento do coeficiente e a redução da complexidade do modelo. Já a Lasso juntamente com os coeficientes de encolhimento, também executa a seleção de recursos. Como observamos anteriormente, alguns dos coeficientes tornam-se exatamente zero, o que é equivalente à exclusão do recurso específico do modelo.

Com os avanços no aprendizado de máquina, a regressão de ridge e lasso oferece alternativas muito boas, pois fornecem uma saída muito melhor, exigem menos parâmetros de ajuste e podem ser amplamente automatizados.

Quanto aos casos de uso típicos, a Ridge é usada principalmente para evitar o overfitting. Como inclui todos os recursos, não é muito útil no caso de #recursos exorbitantemente altos, em milhões, pois representará desafios computacionais. Já a Lasso fornece soluções esparsas, geralmente é o modelo de escolha (ou alguma variante desse conceito) para modelar casos em que os _#features_ estão em milhões ou mais. Nesse caso, obter uma solução esparsa é uma grande vantagem computacional, pois os recursos com coeficientes zero podem simplesmente ser ignorados.

**Tópicos avançados**

Que tal saber mais sobre regressões Lasso e Ridge? Entender como estes funcionam e os tipos existentes são fundamentais para aplicação em análises de predição e classificação. No link abaixo há várias informações sobre os diferentes modos de aplicação e como estas regressões colaboram para o processo de análise. Legal, né?

Para saber mais informações, acessar esse link:

DEVEY, A. Modelos de Predição. Disponível em: < [https://medium.com/turing-talks/turing-talks-20-regress%C3%A3o-de-ridge-e-lasso-a0fc467b5629](https://medium.com/turing-talks/turing-talks-20-regress%C3%A3o-de-ridge-e-lasso-a0fc467b5629)>. Acesso em: 30 de nov. 2022


# Árvores de Regressão