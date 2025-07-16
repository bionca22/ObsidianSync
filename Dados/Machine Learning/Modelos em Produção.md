Neste módulo, vamos falar sobre arquiteturas de modelos em produção, e os conhecimentos iniciais que são necessários para que você tenha um entendimento básico de todo o caminho que um modelo de machine learning percorre para que seja utilizado na produção.

**Resumo**

Antes de tudo, o que significa colocar um modelo de Machine Learning em produção? Bem, qualquer projeto de desenvolvimento de software passa por alguns passos em seu ciclo de vida. Ele começa quando a pessoa desenvolvedora começa a escrever o código propriamente dito e termina quando aquele projeto é disponibilizado para cumprir a função para que foi criado.

Abaixo, temos o ciclo de vida de um projeto de desenvolvimento de software no Uber em que podemos ver as fases por onde se passa até o código estar em produção.

![[Pasted image 20250520182125.png]]
**O que é uma API?**

Um outro conceito muito importante é o de API. A sigla, em inglês, significa Application Programming Interface, que seria interface de programação de aplicação. Isso significa que uma api vai ser um serviço que vai possibilitar a comunicação entre dois ou mais softwares.

Segundo a AWS, “APIs são mecanismos que permitem que dois componentes de software se comuniquem usando um conjunto de definições e protocolos.” Disponível em: [https://aws.amazon.com/pt/what-is/api/](https://aws.amazon.com/pt/what-is/api/)

No contexto de APIs, a palavra Aplicação refere-se a qualquer software com uma função distinta. A interface pode ser pensada como um contrato de serviço entre duas aplicações. Esse contrato define como as duas se comunicam usando solicitações e respostas.

![[Pasted image 20250520182420.png]]

Por exemplo, toda vez que você entra em algum site ou app, existem várias api's trabalhando para buscar informações e trazê-las para você.

![[Pasted image 20250520182506.png]]

**Tipos de Arquitetura**

Podemos dividir uma arquitetura para entrega de resultados de um modelo de Machine Learning em dois tipos: batch e online.

Em uma arquitetura batch, em geral, o modelo é treinado e prevê os resultados de forma offline, salvando em um banco de dados, e uma api é responsável por entregar esses resultados.

Em uma arquitetura online, em geral, o modelo pode tanto aprender quanto prever os resultados de forma online, e uma api é responsável por toda essa comunicação.

![[Pasted image 20250520182557.png]]

**Arquiteturas de Modelos em Batch**

Vamos olhar alguns exemplos de arquiteturas de entrega de resultado de modelos de machine learning que demandam uma natureza offline, como a maioria dos algoritmos de recomendação, classificação e regressão.

Abaixo, temos um exemplo de uma arquitetura para entrega de resultados de modelos de machine learning em batch na AWS. No primeiro passo, os dados estão armazenados em diferentes locais. As input features, por exemplo, geralmente são informações já curadas e poderiam estar em um banco como o Redshift.

A arquitetura abaixo está utilizando o AWS Lambda, que basicamente vai executar um código que irá rodar dentro do serviço de machine learning da Amazon, o Sagemaker (ilustrado como um cérebro na imagem). Esse código irá ler os dados de input e fazer previsões para esses dados, salvando-os no S3, que é o serviço de armazenamento de arquivos da AWS. Note que o modelo que está no S3 já está anteriormente treinado e, por isso, só é necessário fazer as previsões.

Depois, no segundo estágio, os dados de previsão do modelo são armazenados tanto no Data Lake (pode ser um Redshift ou outra solução) quanto no Amazon RDS, que é o banco relacional da AWS.

Assim, para entregar esses resultados para um aplicativo ou um website (client), por exemplo, utilizamos uma api para ler os resultados e entregar para esse client no frontend, como mostrado no estágio 3.

![[Pasted image 20250520182807.png]]

Abaixo, temos um exemplo de uma uma arquitetura, mas agora na Google Cloud Platform (GCP). Da mesma forma, os dados estão em um banco que, no caso, é o BigQuery. De lá, eles são exportados para o Cloud Storage, que é o serviço de armazenamento de arquivos da GCP.

A seguir, esses dados são utilizados como input para o modelo de machine learning, que será executado e gerará as previsões utilizando o Cloud Machine Learning Engine, serviço de machine learning da GCP. Esses dados de previsão do modelo serão salvos novamente no Cloud Storage. Depois, o Cloud Dataflow vai processar esses dados e inserir no BigTable, que é um banco noSql de alta disponibilidade do GCP.

Por fim, para entregar esses resultados para um aplicativo ou um website (client), por exemplo, utilizamos uma api para ler os resultados e entregar para esse client no frontend.

![[Pasted image 20250520182843.png]]

No exemplo abaixo, temos uma arquitetura mais híbrida, onde os resultados que já foram acessados pela api são salvos em um cache, para que a resposta da api seja mais rápida da próxima vez que esse mesmo resultado for pedido pelo client.

![[Pasted image 20250520182911.png]]

**Arquiteturas de Modelos Real Time**

Vamos olhar alguns exemplos de arquiteturas de entrega de resultado de modelos de machine learning que demandam uma natureza online, como os algoritmos de MAB.

Abaixo, temos uma possível arquitetura utilizando a cloud da Azure. Nesse caso, temos dados de ratings de usuários para itens que estão armazenados no Azure Storage (serviço de armazenamento de arquivos da Azure). Com o Azure Databricks, os dados de input do modelo são calculados e salvos no Comos DB, que é um banco noSql de alta disponibilidade da Azure.

Aqui, o modelo de machine learning, que utiliza o Azure Machine Learning Service, já está treinado e rodando dentro de um servidor Kubernets. Quando o client faz uma requisição para o modelo através de uma api, ele pode estar levando informações do usuário, como a sua localização.

Por fim, o modelo lê os inputs do Cosmos DB, usa as informações passadas pela api e gera um resultado, que é entregue novamente para o client por uma api.

![[Pasted image 20250520182937.png]]

Aqui, temos outra arquitetura online, agora usando a Google Cloud Platform. Nesse caso, os dados de input do modelo estão no Datastore, que é um banco de dados NoSQL de alto desempenho da GCP.

Nessa arquitetura, toda vez que o client faz uma requisição, a api usa o entityId (pode ser o Id anônimo do usuário), coleta as informações de input no Datastore para então passar para o modelo de machine learning, que está sendo executado na Machine Learning Engine que, por sua vez, irá gerar os resultados de previsão que, por fim, serão passados para o client. Vale dizer que, nesse caso, o modelo já está treinado.

![[Pasted image 20250520183002.png]]

Por fim, temos uma arquitetura de entrega de modelos online utilizando a AWS. Aqui temos 3 camadas diferentes. Na primeira, temos a ingestão de dados, onde é feita toda a modelagem e tratamento dos dados, de forma a ficarem prontos e serem consumidos pelo modelo de machine learning. Esses inputs são salvos na Amazon Redshift.

A seguir, temos a segunda camada, onde acontece o treinamento do modelo de machine learning. Nessa arquitetura, o modelo está sendo constantemente re-treinado com os novos dados que ficam disponíveis. Assim, garantimos que o modelo está sempre ajustado com os dados mais recentes e esperamos uma melhor performance por isso. É então feito o deploy do modelo treinado para o Sagemaker.

Na terceira e última camada, o client se comunica com o modelo, que está no Sagemaker, através de uma api, que aciona um Lambda. Este vai levar os dados da requisição do client (id de usuário, localização, tela do app, etc) até o Sagemaker, para que o modelo de machine learning já treinado faça suas previsões. O resultado então é devolvido para o client.

![[Pasted image 20250520183048.png]]

**Como aplicar na prática o que aprendeu**

Primeiro de tudo, é importante entender qual a natureza do seu modelo e se uma arquitetura em batch é suficiente para que se tenha o resultado esperado. Em geral, arquiteturas em batch são menos custosas e mais performáticas, o que facilita bastante sua adoção.

Além disso, procure entender na sua empresa qual o processo para que um modelo vá para produção. É importante saber qual cloud a empresa usa, quais ferramentas já estão à disposição e até mesmo se existe uma equipe que possa te auxiliar com essa tarefa.

**Tópicos avançados**

Dependendo da empresa e do contexto em que você estiver inserido, mais ou menos conhecimento dos detalhes de cada parte da arquitetura vai ser exigido de você.

Por isso, é importante conhecer algumas ferramentas que já se tornaram padrão de mercado, como o **S3**,  **Sagemaker da AWS**, o **Kafka da Apache** (open source), o que é um **data lake** e o que é um orquestrador de workflows, como o **Airflow** (o mais utilizado hoje em dia).

Seguem abaixo os links das ferramentas para que possam se aprofundar no assunto:

[https://www.aquare.la/apache-airflow-o-que-e-e-como-funciona/](https://www.aquare.la/apache-airflow-o-que-e-e-como-funciona/)

[https://aws.amazon.com/pt/big-data/datalakes-and-analytics/what-is-a-data-lake/](https://aws.amazon.com/pt/big-data/datalakes-and-analytics/what-is-a-data-lake/)

[https://www.redhat.com/pt-br/topics/integration/what-is-apache-kafka](https://www.redhat.com/pt-br/topics/integration/what-is-apache-kafka)

[https://www.treinaweb.com.br/blog/o-que-e-aws-s3](https://www.treinaweb.com.br/blog/o-que-e-aws-s3)