**Introdução**

Para entender a importância do processo de coleta e tratamento de dados, é preciso saber as etapas do processo de descoberta do conhecimento. Para tal, é necessário entender a diferença entre dados, informação e conhecimento.

**Objetivos da aula**

- Saber diferenciar dados x informação x conhecimento;
- Saber quais são as fases para descobrir o conhecimento através dos dados;
- Identificar onde a coleta de dados está inserida no Processo ETL;
- Conhecer os tipos de fontes de dados e planejar as possíveis extrações.

**Resumo**

**Dado – Definição**

É a menor unidade de armazenamento dentro de um banco de dados. É um aspecto que quando “olhado” sozinho não tem significado, não tem sentido. Para que haja compreensão do dado, é sempre necessário fazer o processamento, a realização de algum tipo de operação com o dado.

Figura 1: Exemplo de dados
![[Pasted image 20250412073034.png]]
**Informação – Definição**

A informação é o resultado de algum tipo de operação com o dado, ou seja, é sempre através do processamento dos dados que se pode obter a informação. Veja:

Figura 2: Exemplo de informação
![[Pasted image 20250412073106.png]]
**Conhecimento – Definição**

Ocorre quando utilizamos a informação para chegar a alguma conclusão, ou até mesmo, reconhecer algum tipo de comportamento e/ou padrão.

Através de análises estatísticas, por exemplo, média, contagem, valor máximo, valor mínimo e taxas de porcentagem das informações, chega-se ao conhecimento.

Leia este exemplo: Como o dia está quente e a probabilidade de chover é baixa, irei à praia.

Uma loja de roupas de praias, usando esse conhecimento, pode reforçar seu estoque, ou enviar comunicações de promoções, ou ainda criar ações de marketing, entre outros.

**Etapas do Processo de Descobrimento do Conhecimento**

Para se chegar ao conhecimento, primeiro é necessário coletar os dados, depois se faz todo o processo de transformação desses dados chegando ao momento da mineração, onde realizam-se diversos tipos de análises, para então se alcançar o conhecimento, conforme figura 3.

Analisando a figura 3, percebe-se a importância da coleta e tratamento de dados, pois sem eles não há como chegar ao conhecimento.

Figura 3 - Etapas do Processo de Descobrimento do Conhecimento

![[Pasted image 20250412073147.png]]
**Planejamento da Coleta de Dados**

A primeira fase tem por objetivo definir o escopo do projeto, prestando atenção nas áreas críticas da empresa e as carências mais perenes de informações gerenciais.

As preocupações são em definir como será o desenvolvimento e quais os setores de principais temas. Ao desvendar as respostas para estas preocupações, consegue-se a determinação do que deverá ser realizado no projeto.

Com isso, utilizam-se habilidades de levantamento de dados e análise prévia. O ideal aqui é conseguir estabelecer um meio termo entre o desenvolvimento gradual dos projetos de Data warehouse e a definição de dimensões conformes, que permitam a integração gradativa de Data warehouse, sem agigantamento de projetos. O conhecimento sobre a engenharia tecnológica base é fundamental, pois, durante o projeto, problemas como: desempenho e disponibilidade poderão afetar o cumprimento do projeto.

As ferramentas básicas de tecnologia como SGBD (Sistema Gerenciador De Banco De Dados), Metadados, Ferramentas De Desenvolvimento Olap (_Online Analytical Processing_) e Processo de ETL (extração, transformação e  carga) deverão ser analisados, além da rede empresarial.

Figura 4 - Visão Geral do Sistema

![[Pasted image 20250412073219.png]]

É relevante analisar que os dados a serem modelados deverão ser coletados nos seus vários níveis de detalhes e o modelo relacionado com as fontes dos dados onde deverão ser registrados os conceitos de dados existentes, com suas respectivas descrições, formas atuais de armazenamento e de uso nos sistemas. A qualidade e a integridade da fonte de dados devem ser analisadas com muita atenção, além do tempo histórico dos dados.

**A Coleta de Dados dentro do Processo ETL(C) – Extração, Transformação e Carga**

Nesse momento, os significados de extração dos dados e de seu tratamento podem ser divididos em:

- **Filtro de Dados:** relaciona os modos e situações para se eliminar os elementos de dados inconvenientes no modelo dimensional. Por exemplo, almeja-se que somente pedidos de vendas com valores superiores a U$ 2.500,00 sejam consideradas no sistema gerencial em projeto.
- **Integração de Dados**: define a forma de se concatenar informações existentes em fontes diferentes e que deverão ser adaptadas no sistema gerencial. A adaptação dessas informações torna-se essencial para os requisitos do sistema e deverá ser previsto nessa etapa. Como padrão, poderia ser o caso de dados que estão codificados em um ambiente (por exemplo, o código do fornecedor junto com o código da  região) e que deverão ser codificados, a fim de facilitar o seu uso, relacionando-se a ele um dado explícito sobre região.
- **Condensação de Dados**: define o molde de se diminuir volumes de dados visando obter informações resumidas e totalizadas. Como exemplo, temos a sumarização em termos semanais de dados diários de compras, ou o resumo em níveis geográficos, por exemplo, vendas por região.
- **Conversão** de **Dados:** define os métodos para se alterar dados em unidades, moldes e dimensões diferentes.
- **Derivação de Dados**: define os meios e fórmulas para gerar dados virtuais, a partir de dados presentes.

Figura 5 - Fontes de Dados
![[Pasted image 20250412073307.png]]
o do mesmo nome várias vezes e garantindo que o nome da cidade esteja escrito sempre do mesmo jeito para todos os clientes.

No caso do banco de dados que passou pelo processo da desnormalização, vamos encontrar o nome da cidade registrado na tabela de clientes, uma vez para cada cliente que morar naquela mesma cidade, o que aumenta muito o tamanho do banco de dados e não certifica a consistência deles

----
![[Pasted image 20250412073712.png]]


#### **Coleta e Extração de Dados**

Para compreender a carência dos processos ETL, primeiramente, é indispensável compreender onde esses processos são introduzidos e os motivos pelos quais são indispensáveis. Por esse fator, antes de qualquer coisa, é significativo falar sobre BI (_Business Intelligence_ - Inteligência de Negócio).

O termo Business Intelligence (Inteligência de Negócio) foi empregado em 1989 pelo Gartner Group, que defendeu a criação do termo para abrigar todas as iniciativas de inteligência. Com a mundialização, o mundo ficou mais competitivo, as organizações corporativas e clientes ficarão muito ágeis e exigentes, por isso, torna-se indispensável o tratamento e a sincronização dos dados, para apoio às decisões e manter as organizações corporativas com alto grau de competitividade.

Os dados assumem um papel essencial para a conquista de lucros nos negócios. Diante da grande quantidade de dados que são produzidos no momento, é indispensável determinar os critérios para seleção e organização dos dados considerados significativos.

Business Intelligence pode ser definido como um grupo de estratégias utilizadas para extrair inteligência, a partir de dados sobre um determinado negócio.  Consiste no processo de transformar dados em informação e através dessa descoberta, transformar informação em conhecimento.

O foco é converter o volume de dados em dados referentes ao negócio, através de relatórios analíticos. O plano é sempre de extrair Inteligência dos dados. Quanto maior o volume, menor é a competência analítica sobre uma massa de dados. Por exemplo: analisar todas as compras classificadas pelas ruas dos seus clientes ou analisar as vendas por bairro da sua cidade.

O dado utilizado para a tomada de decisão sempre é uma visão simplificada do total das informações disponíveis.

**Tática para Construção de Sistemas BI (Inteligência de Negócio)**

A maior estratégia é a montagem de um Data Warehouse para a organização dos dados. As conveniências da montagem do DW é a criação de um ambiente para inclusão e tratamento dos dados. O ambiente com foco único e a separação dos sistemas legados (transacionais). A Base de dados otimizada para consultas e a Sustentação de ferramentas específicas para esse fim.

Data Warehouse é um procedimento que coleta os dados de sistemas operacionais e transacionais, limpando, transformando em dados organizados, permitindo análises dessas informações. Seus principais criadores e autores são: Ralph Kimball e Bill Inmon.

Segundo William Inmon, um dos criadores desta tecnologia Data Warehouse é um grupo de dados orientado por assuntos, não volátil, variável com o tempo e integrado, gerados para dar sustentação à decisão.  
Orientação por assunto: é o encaminhamento que se tem da visão que será disponibilizada, do negócio da organização corporativa, por exemplo: numa organização corporativa de comércio eletrônico, o assunto fundamental são os clientes, que podem ser: residenciais, organizações corporativas, telefonia pública, etc. Então, quando um analista de DW for conceber o modelo do mesmo deve ter atenção com essas premissas, e dividir as visões de acordo com o que o tomador de decisões quer visualizar. É significativo ressaltar que tudo será orientado pelos assuntos, seja qual for a visão que se quer ter, ou seja, a visão financeira da organização corporativa também irá se preocupar em torno disso, seja a inadimplência, o faturamento, a lucratividade, etc.

Volatilidade: refere-se ao DW não sofrer alterações como nos sistemas tradicionais, por exemplo, no sistema de cadastro de faturas de uma organização corporativa, todos os dias ocorrem inclusões e alterações de novos clientes, novos produtos e consumo. No Data Warehouse ocorrem somente cargas de dados e consultas, ou seja, há somente selects (consultas) e inserts (inserções) e não há updates (atualizações). Em resumo, num sistema de apoio à decisão existem basicamente duas operações: a carga(inserts de grandes volumes) e consulta (select).

Variável com o tempo: é uma qualidade do DW. Ele sempre retrata a situação analisada, num determinado instante de tempo, por exemplo, pegue uma fotografia sua quando recém-nascido e, depois, pegue outra quando você tinha 15 anos de idade e faça a comparação. Com certeza muitas modificações ocorreram, mas ela retrata exatamente a sua situação naquele exato momento do tempo. Isso acontece do mesmo jeito com o DW. São guardadas “fotografias” dos assuntos em determinados instantes de tempo e, com isso, é permitido determinar uma análise histórica e fazer comparação entre os fatos ocorridos.

Inclusão: é responsável por conciliar os dados de todos os sistemas existentes na organização corporativa, além de colocá-los no mesmo padrão. O DW coleta dados de vários sistemas da organização corporativa e, em alguns casos, dados externos. Porém, geralmente os dados não estão no mesmo padrão, então é indispensável integrar antes de fazer a carga no DW.

**Atividades para implementação do Processo ETL**

- Determinar onde os dados serão armazenados e analisados;
- Determinar como procurar os dados nas fontes (ERP,CRM,etc);
- Montar os processos de carga, acumulação e análise.
- Determinar como os dados serão organizados para o BI;
- Qual o grau de detalhamento será armazenado;
- Determinar junto às padronizações necessárias para a estrutura de dados;
- Determinar qual banco de dados será utilizado para acumulação de dados;
- Determinar qual será o período de alterações dos dados;
- Determinar como os dados serão coletados dos sistemas;
- Determinar como os dados, nos sistemas fontes serão disponibilizados.

![[Pasted image 20250413071046.png]]

Os focos do Processo ETL são: coletar, limpar, padronizar e carregar os dados no Data Warehouse, ou seja, permitir que os dados estejam prontos para consulta.

![[Pasted image 20250413071118.png]]

Os projetos de Data Warehouse firmam dados de diferentes fontes. Grande parte dessas fontes tem a tendência a ser bancos de dados relacionais ou outros tipos de arquivos, mas podem existir outros tipos de fontes também. Um sistema ETL precisa ter a capacidade de se conectar com bancos de dados e ler uma variedade de formatos de arquivos utilizados por toda a empresa.

**Requisitos para o Projeto ETL**

Antes de iniciar um Projeto de ETL, é indispensável que os seguintes elementos estejam bem determinados:

- **Exigências de negócio:** ter bem claro e documentado quais são as exigências de negócio;
- **Viabilidade dos Dados:** realizar um estudo de viabilidade dos dados;
- **Latência dos Dados:** determinar o tempo máximo permitido para  disponibilização dos dados através do sistema de BI.
- **Políticas de Compliance e Segurança:** Determinar quais são as políticas de compliance e segurança usadas.

**Relevância do Processo ETL**

O processo de ETL é fundamental para a geração das estruturas de dimensões e Fatos no ambiente do DW. Esse processo é responsável por fazer a ligação entre o operacional e o DW. Deve-se selecionar bem as ferramentas que darão sustentação ao processo, pois são essenciais para a correta execução das atividades do ETL.

O ETL é essencial para qualquer iniciativa de DW. Contudo, deve ser planejado com cuidado para não comprometer os sistemas de processamento transacional (OLTP) das organizações corporativas. Um bom ETL deve ter escalabilidade e ter a capacidade de sofrer manutenções. 

Além disso, deve-se analisar o período de tempo para realização da operação do ETL, pois não é em qualquer momento que ele poderá ser acionado. Do mesmo modo, é indispensável analisar a periodicidade de execução, como também determinar qual será o alcance de dados que o ETL abrangerá. Esses detalhes são analíticos para o sucesso do processo.

O ETL une e permite a direção dos dados ao DW. O processo deve ser bem planejado para evitar possíveis transtornos no futuro e até mesmo para que não ocorra, em casos extremos, a parada dos sistemas operacionais da organização corporativa. Dessa forma, o DW terá dados tratados, com qualidade e grande valor para sustentar as decisões organizacionais.

**Principais Elementos do ETL**

Na figura 3 é possível visualizar um exemplo de modelo de Arquitetura de uma solução de BI.

Figura 3 - Arquitetura de Solução BI

![[Pasted image 20250413071158.png]]

**Definição das Etapas ETL ou ETC (Extração, Transformação e Carga)**

**E – Extração:** coletar os dados de sistemas legados; muitas podem ser as fontes de dados, por exemplo, banco de dados relacionais, sistemas ERP, redes sociais, vídeos, áudios, planilhas, documentos, etc. Essa coleta leva os dados para uma área de trabalho chamada de staging area. Essa área serve para que se possa trabalhar e executar táticas aos dados coletados. É a coleta de dados dos sistemas de origem (também chamados Data Sources ou sistemas operacionais), extraindo-os e transferindo-os para o ambiente de DW, onde o sistema de ETL pode ser executado independente dos sistemas operacionais (ambiente OLTP).

A etapa de extração pode ser entendida como a fase em que os dados são coletados dos OLTPs e conduzidos para a staging area (área de transição ou área temporária), onde são convertidos para um único formato. Essa mudança se faz necessária devido à diversidade existente nos dados originados desses sistemas, sendo essencial a configuração antecipada para o tratamento apropriado.

Para realizar a coleta dos dados, deve-se fazer a definição das fontes de dados e fazer a extração deles. As origens deles podem ser várias e também em diferentes formatos, podendo achar desde os sistemas transacionais das organizações corporativas até planilhas, flat files (arquivos textos), dados do Mainframe, dados das redes sociais, etc.  
 

**T – Transformação:** transformar, limpar, modificar o dado. É nesta fase que se executam as necessárias alterações, podendo assim otimizar a qualidade dos dados e fortalecer dados de duas ou mais fontes. A etapa de transformação aplica uma série de normas ou funções aos dados coletados para arrumar os dados a serem carregados. Algumas fontes de dados precisarão de pouca modificação. Em outras situações, podem ser indispensáveis trabalhar algumas transformações, por exemplo, ligação de dados provenientes de diversas fontes, escolha de apenas determinadas colunas e Tradução de valores codificados (se o sistema de origem armazena “Masc” para sexo masculino e “Fem” para feminino, mas o data warehouse armazena M para masculino e F para feminino, por exemplo).  Outro exemplo da carência de transformação dos dados, é muito comum, na obtenção dos dados que, no mais das vezes, são antigos e desconhecidos, acharmos muito ‘lixo’ e inconsistências. Quando um vendedor de telefones for executar uma venda, ou inscrição, ele está preocupado em vender, e não na qualidade dos dados que está incluindo na base, então, se por acaso o cliente não tiver o número do CPF, ele insere um número qualquer, desde que o sistema aceite, um dos mais utilizados é o 999999999-99. Agora, imagine um diretor dessa mesma organização corporativa consultar o seu DW para ver quais são os seus maiores clientes e aparecer em primeiro lugar o cliente que tem o CPF 999999999-99, ou seja, um dado inconsistente. Por isso, nessa fase do DW são corrigidos, padronizados e tratados os desvios e inconsistências, transformando os dados de acordo com as regras do negócio.

**L/C – Load ou Carga dos dados:** preparar e carregar os dados no Data Warehouse e/ou Data Mart para serem apresentados. Corresponde em estruturar e inserir os dados para dentro da camada de apresentação seguindo o modelo dimensional.

Dependendo das carências da organização, este processo varia amplamente. Alguns data warehouses podem trocar os dados existentes semanalmente, com dados totalizados e atualizados, ao passo que outro DW (ou até mesmo outras partes do mesmo DW) podem carregar dados a cada hora. O atraso de tempo e o alcance de reposição ou acréscimo constituem opções de projetos estratégicos que dependem do tempo disponível e das carências de negócios. A etapa de carga ocorre depois da execução da fase de transformação. Assim que são efetuados os tratamentos indispensáveis nos dados, a carga no DW é iniciada. Essa fase se resume na perseverança dos dados na base fixa.

A etapa de Gerenciamento é formada por serviços para ajudar na administração do Data Warehouse. Tarefas próprias para administração de jobs, planos de backup, verificação de itens de segurança e compliance (regras e políticas).

**Conteúdo bônus**

**Tópicos avançados**

Chuck Ballard, Daniel M. Farrell, Amit Gupta, Carlos Mazuela, Stanislav Vohnik; **Dimensional Modeling: In a Business Intelligence - Inteligência de Negócio Environment;** An IBM Redbooks publication;2012

Chapter 1. Introduction

Chapter 2. Business Intelligence - Inteligência de Negócio: The destination

Nesta publicação, IBM Redbooks descreve as táticas de modelagem de dados dimensionais, especificamente focadas em Business Intelligence e data warehousing. É para ajudar o leitor a entender como projetar, manter e usar um modelo dimensional para data warehousing que pode fornecer acesso e desempenho de dados indispensáveis para a inteligência de negócios.

A inteligência de negócios é composta por uma arquitetura de data warehouse e um ambiente de consulta, análise e geração de relatórios. Aqui, concentra-se na infraestrutura de data warehousing. Contudo, apenas um elemento específico disso, o modelo de dados que é considerado o princípio básico de desenvolvimento do data warehouse, ou, mais precisamente, o tema da modelagem de dados e seu impacto nas aplicações comerciais e organização corporativa. O foco não é fornecer um tratado sobre estratégias de modelagem dimensional, mas focar em um grau mais prático. Existe conteúdo técnico para projetar e manter esse ambiente, mas também conteúdo comercial.

São usados estudos de caso para demonstrar como a modelagem dimensional pode afetar as exigências de Business Intelligence - Inteligência de Negócio para suas iniciativas de negócios. Além disso, é fornecida uma discussão detalhada sobre os aspectos da consulta de BI e modelagem de dados. Por exemplo, é demonstrada a otimização de consulta e como se pode determinar o desempenho do modelo de dados antes da implantação.


## Carga de Dados Limpos 

**Introdução**

Conhecer o processo de Load (Carga) dos dados; Identificar os objetivos de Data Warehouse, Data Mart e construir alguns exemplos de dashboards. Compreender e vivenciar na prática as etapas de desenvolvimento de um projeto de Data Warehouse, utilizando ferramentas Olap.

**Resumo**

Construir um projeto de Data Warehouse não é uma missão fácil. São necessários muitos passos para atingir esse objetivo. Para executarmos essa tarefa, podemos seguir dois caminhos, que são eles: manual ou com uso de ferramentas. Claro que cada um deles tem vantagens e desvantagens. Vamos explorar o uso de ferramentas. As vantagens do uso delas é que torna o processo muito mais fácil de implantar, fácil de interagir, a possibilidade de criação de vários tipos de relatórios com diferentes tipos de gráficos e de forma rápida, além das muitas opções de edição de consultas e também o processo de obtenção de dados é facilitado, pois a ferramenta possui vários módulos de conexões com diferentes tipos de ambientes e infraestrutura. No entanto, as desvantagens são: o custo da compra da licença e a manutenção. Além disso, você está nas mãos da ferramenta. Se algo parar de funcionar, não terá controle sobre o que está acontecendo e nem em que deve mexer para fazer uma possível atualização, por exemplo. Trabalhar com ferramentas para implementação de um projeto de Data Warehouse são alguns dos itens mais requisitados para profissionais que sejam administradores, analistas de BI.

 
 **Implementação do projeto de DW  Com o uso de Ferramentas**

As ferramentas escolhidas deverão possibilitar a definição de aplicativos com interfaces amistosas, geradores de relatórios, condições de visualização de dados em formas variadas e a importação dos dados obtidos para ferramentas do usuário final, como planilhas e processadores de textos. O conjunto de ferramentas dedicadas ao desenvolvimento de aplicações são chamadas OLAP (_Online Analytical Processing)_.

O _Data Mining_ é extremamente adequado para analisar grupos de dados que seriam difíceis de analisar usando apenas a função Olap (Online Analytical Processing_)_, haja vista, que esses grupos são grandes demais para serem “navegados” ou explorados manualmente, ou ainda porque contêm dados muitos densos ou não-intuitivos para serem compreendidos.

A diferença básica entre olap (on line analytical processing) e _data mining_ está na maneira como a exploração dos dados é realizada. Na análise olap (online analytical processing) a exploração é feita através do analista, enquanto que a análise _data mining_ é feita pela própria ferramenta.

As vantagens de se usar as ferramentas etl são: a programação gráfica é baseada em parâmetros, a lógica é transparente e de alto nível, a documentação é gerada de forma automática, a geração e o suporte aos dicionários de dados é automático, procedimentos de agendamento de tarefas, biblioteca de conectores com banco de dados e arquivos, procedimentos para balanceamento de carga e paralelismo, controle de versão de mudanças. O mercado possui vários cursos a respeito e profissionais para trabalhar com essas ferramentas. Como desvantagens podemos citar: o custo muito elevado, além de não serem ferramentas simples de manusear. Portanto, necessitam de uma grande dedicação para aprendizagem.

 **Principais funções de Transformação de ferramentas OLAP**

Para realizar a etapa de transformação, muitas funções e de diferentes tipos são necessárias. Nas ferramentas ETL pode-se encontrar as seguintes funções: agregações, construção de consultas com expressões gerais, consultas com vários tipos de filtros e  joins, várias formas de “procurar” lookups dados, formas para ajustar dados “normalizers”, várias formas de ordenação “rankers” , geradores de sequência, adaptadores, procedures criadas e armazenadas, leitores e geradores de arquivos xml, além de diversas facilidades para desenvolvimento de código próprio.

##### Principais players de mercado de ferramentas ETL:

- Informatica PowerCenter;
- Oracle Warehouse Builder;
- BO Data Integrator;
- Power BI da Microsoft;
- Cognos Decision Stream;
- IBM Data Stage;
- Microsoft SQL Server DTS;
- SAS Enterprise ETL Server (mais utilizada nos projetos que utilizam o SAS Studio) ;
- Oracle Data Integrator é uma poderosa ferramenta de integração adquirida da Sunopsis.


**Características do Power BI**

É uma ferramenta que permite transformar as fontes de dados não relacionadas em informações coerentes, de forma visual, interativas e independente do formato e/ou localização dos dados; pode ser uma planilha do Excel ou uma coleção de d_ata warehouses_ híbridos baseados em nuvem e locais. O Power BI possibilita uma conexão fácil às fontes e visualização dos dados. Além de ser uma ferramenta com conexão a vários tipos de ambientes, como desktop, plataformas mobile e nuvem.

Os blocos de construção básicos no Power BI são os seguintes:

- **Visualizações**: É uma representação visual dos dados, como um gráfico, ou outras representações gráficas.
- **Conjuntos de dados**:  é uma coleção de dados usada para criar visualizações. Podem ser uma combinação de várias fontes diferentes, que podem ser filtradas e combinadas para fornecer dados. Por exemplo,  um conjunto de dados que tem três campos de banco de dados diferentes, uma tabela de site, uma tabela do Excel, toda essa combinação forma um único **conjunto de dados**.
- **Relatórios**: um **relatório** é uma coleção de visualizações que aparecem juntas em uma ou mais páginas. Assim como ocorre com qualquer outro relatório que você possa criar para uma apresentação de vendas ou um relatório que você prepararia para uma tarefa escolar. É uma coleção de itens que estão relacionados entre si. 
- **Painéis**: quando você está pronto para compartilhar uma única página de um relatório ou compartilhar uma coleção de visualizações, você cria um **dashboard**. Assim como o painel de um carro, um **dashboard** é uma coleção de visuais de uma única página. Geralmente, é um grupo selecionado de visuais que fornecem uma análise rápida dos dados ou da história que está sendo apresentada.
- **Blocos**: é uma única visualização encontrada em um relatório ou dashboard.  É a caixa retangular que contém cada visual individual. Ao _criar_ um relatório ou um _dashboard_ é possível mover ou organizar os blocos, a fim de apresentar informações.

**A SEGUIR UM EXEMPLO**
 ![[Financial Sample.xlsx]]
Sendo que as colunas da planilha são: Segment (Segmento), Country(País), Product (Produto), Discount Band (margem de desconto), Units Sold (unidades vendidas), **Manufacturing Price** (preço de fabricação), Sale Price(Preço de Venda), Gross Sales (Vendas Brutas), Discounts (Descontos), Sales (Valor das Vendas),  COGS  Profit (lucro), Date (Data), Month Number (número do mês), Month Name (Nome do Mês), Year(Ano).

Amostra da planilha:

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674836514025-h0zF0iwYuP.png "Fonte: Autoral, 2022")
Crie consultas ao importar dados a partir de uma nova origem:

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674836547123-1Eg7AuJOHl.png "Fonte: Autoral, 2022")

1. Abra o Power Bi

2. Clique em obter Dados

3. Selecione **Arquivos**.

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674836595281-JFZuUDH6rm.png "Fonte: Autoral, 2022")

4. Navegue até o arquivo no seu computador e escolha **Abrir**. 

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674836631259-Sfq0AEuYLW.png "Fonte: Autoral, 2022")

Clique em carregar

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674836664803-YO90cOmD5u.png "Fonte: Autoral, 2022")
**Edição de Consultas – Transformação de Dados**

Clique em Editar Consultas para visualizar os dados carregados

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674836698425-FtN4LbykvD.png "Fonte: Autoral, 2022")

Nesta seção, é possível fazer todas as alterações nos dados, por exemplo, para formatar os dados clique em formatar e depois em maiúsculas:

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674836757382-sC4GvgniaX.png "Fonte: Autoral, 2022")

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674836819978-dakiV7qE1p.png)

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674836854166-M6L0ihiOmb.png "Fonte: Autoral, 2022")


Para alterar os nomes das colunas, clique em mudar o nome. Por exemplo, de units sold para unidades vendidas.

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674837051408-JPCI6AxrRD.png)

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674837060165-TEoAFQlqmG.png "Fonte: Autoral, 2022")

Para fazer as transformações dos dados:

Por exemplo, vamos trocar na coluna discount band o valor None por Nenhum.

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674837109346-vQ6xNkj8mC.png "Fonte: Autoral, 2022")


Para fazer agrupamentos de dados, selecione a coluna e clique em agrupar por:

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674837135510-zdthUVYieb.png "Fonte: Autoral, 2022")

Para fazer operações aritméticas, clique em padrão e depois em porcentagem:

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674837160386-F9ul92kbwq.png)

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674837166399-obGZ5JtkZ2.png)

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674837173589-rs5lju9Njw.png "Fonte: Autoral, 2022")

Para gerar análises estatísticas, entre outras, clique em estatísticas e depois em soma:

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674837215348-J4wZvdm96F.png)

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674837225829-j2oISFXxRi.png)

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674837238271-IV09VwtNBR.png)

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674837244231-ss1ThMAnAH.png "Fonte: Autoral, 2022")


**Visualizações de Dados – Montagem do dashboard**

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674837410049-ojWAMILTkn.png "Fonte: Autoral, 2022")

No menu à direita, escolha o gráfico em barras e arraste para a área de relatório. Depois, arraste os campos que deseja visualizar no gráfico, por exemplo, vendas brutas por ano.

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674837435291-mpjXwCmZNn.png "Fonte: Autoral, 2022")

**Geração de Relatórios**

Na área de relatório, selecione a tabela, o campo produto, vendas e nome do mês:

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674837481948-28PBXbStGR.png "Fonte: Autoral, 2022")

Clique no gráfico de pizza e selecione os campos país e discounts.

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674837503631-1a8XCy0VQp.png "Fonte: Autoral, 2022")

Média de Lucro por País representado no gráfico de Pizza

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674837814377-YWp1zG32Lq.png "Fonte: Autoral, 2022")

Clique em mapa de manchas e selecione os campos country e profit (lucro por países)

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674837834094-YtaomQnerg.png "Fonte: Autoral, 2022")

Dessa forma, selecionando as visualizações, o dashboard é montado.

Como podemos verificar, trabalhar com o Power BI é bem intuitivo e fácil de interagir. É importante ressaltar que o TRABALHO não está em interagir com a ferramenta ou na montagem do dashboard, mas sim em dizer quais são os dados relevantes, que relatórios/gráficos devem ser apresentados para atender a estratégia empresarial, quais dados vão dizer as tendências de investimos, vendas, estoque, enfim, atender o objetivo maior de apoiar a tomada de decisão. Por tudo isso, é fundamental ressaltar que a ferramenta é apenas isso, uma ferramenta, o que realmente importa é a estratégia de DW, a modelagem dimensional e traçar corretamente os processos ETL. Se estas fases estiverem claramente definidas, a implementação do projeto de _Data Warehouse_ com a ferramenta será executada com perfeição.

**Tópicos Avançados**

**Execução de um exemplo prático passo-a-passo – Projeto de _Data Warehouse_**

1º Passo) Selecionando as fontes dos dados no ambiente OLTP

Nossas fontes de dados são 2 tabelas (Empregados e Departamentos) que encontram-se no ambiente OLTP.

- visualização dos dados da tabela employees

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674837914496-TObK3UsGu6.png "Fonte: Autoral, 2022")

- visualização dos dados da tabela departments

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674837940075-kUHGropV1j.png "Fonte: Autoral, 2022")

Pronto, seu ambiente OLTP está montado. Essas serão as fontes de dados que vamos trabalhar nos próximos passos. 2º Passo) Definição de quais são relevantes para a estratégia do DW e geração de relatórios.

Na tabela de employees do schema HR (empregados) temos os seguintes campos:

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674838029738-6bt1X7YD7r.png)

Depois de analisarmos a estrutura das nossas fontes de dados, é necessário selecionar desse grupo, quais dados são relevantes para o DW, ou seja, quais dados serão utilizados para serem gerados os relatórios e as estatísticas para tomada de decisão.

Nesse exemplo, nossa escolha de dados relevantes é: código do funcionário, sobrenome do funcionário, salário, data de admissão, código do departamento e nome do departamento.

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674838070456-JZPNnBgrMg.png "Fonte: Autoral, 2022")

3º Passo) Montagem da Staging Area – Extração e Transformação dos dados

Nunca devemos alterar os dados do ambiente OLTP. Para fazer a extração de dados, podemos criar outro banco de dados, outro tablespace. Contudo, para levar os dados, podemos utilizar o recurso de uma view que tem como tabelas-base empregados e departamentos, conforme o comando abaixo:

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674838107231-FVnEXLG5AQ.png)

É neste momento que, se necessário, também se realizará a transformação de dados.

Seleção dos dados da view staging_area

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674838340518-CF3Hg5hZam.png "Fonte: Autoral, 2022")

**- Transformação de Dados**

A transformação de dados consiste basicamente no uso do comando update, alterando os dados para o padrão desejado.

Exemplo 1: na base de dados existe o campo sexo com vários valores, como: mulher, feminino, f, F. Supondo que o valor padrão seja “F”, basta fazer o seguinte comando:

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674838457032-V8DXCxePKf.png)

Exemplo 2: quando consta nulos no campo para realizar a transformação, basta executar o comando abaixo:

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674838509794-Q25cThyfJC.png)

4º Passo) Preparação do ambiente OLAP – Tabela destino 

Para se fazer a carga de dados, todos os objetos do ambiente do DW devem estar criados e preparados, conforme se vê no comando abaixo.

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674838562864-nrGof1MZ9Q.png)

5º Passo) Realização da Carga de dados

Na realização da carga de dados precisamos adequar os tipos dos dados, os nomes dos campos  entre origem (Staging Area) e destino (Tabela do DW), a ordem em que os dados estão dispostos na origem e como os campos serão disponibilizados no destino.  Verifique o comando abaixo:

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674838602817-BOR77HCus2.png)

6º Passo) Ajustando a Surrogate Key

É necessário criar uma chave primária “falsa” para identificar o registro no ambiente de DW. Por esse motivo, precisamos ajustar a SK na tabela, conforme comandos abaixo:

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674838637275-YogproBUgi.png)

7º Passo) Visualização dos Dados e Geração de Relatórios

  
Relatório de todos os empregados e seus respectivos departamentos:

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674838669746-ar21ND0Li9.png)

Relatório de todos os empregados e seus respectivos departamentos

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674838714361-Ry4UyfrJzF.png "Fonte: Autoral, 2022")
Relatório da Soma Salarial e total de empregados por departamento

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674838739682-4xh7tBf3bC.png)

Relatório da Soma Salarial e total de empregados por departamento

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674838777540-T2wNhrCJAD.png "Fonte: Autoral, 2022")

Relatório de custos por departamento e subtotal

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674839328683-vPcr4cwfdl.png)

Relatório de custos por departamento e subtotal

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674839351284-hXOgrzeaxN.png "Fonte: Autoral, 2022")

Para cada comando e/ou relatório você pode criar uma procedure como o exemplo da figura acima, com o objetivo de agilizar o processo.

Caro estudante, você consegue acessar os códigos utilizados na disciplina no link a seguir: [https://github.com/FaculdadeDescomplica/ColetaeTratamentodeDados](https://github.com/FaculdadeDescomplica/ColetaeTratamentodeDados)