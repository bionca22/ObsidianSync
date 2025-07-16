
**Introdução**

Aprenderemos as técnicas e ferramentas para realizar coleta de dados nas principais fontes de dados estruturados (dados localizados em banco de dados relacionais), semiestruturados (dados localizados em arquivos TXT) e não-estruturados (por exemplo, imagens).

**Objetivos da aula**

- Conhecer exemplos de fontes de dados estruturados;
- Conhecer exemplos de fontes de dados semiestruturados;
- Conhecer exemplos de fontes de dados não-estruturados;
- Conhecer o processo de extração dos diferentes tipos de fontes de dados;
- Conhecer ferramentas para realização de extração de dados.

**Resumo**

**Fonte de Dados Não Eletrônicos**

São os registros manuais, dados localizados em documentos, livros, cadernos, apontamentos em pedidos de papel, etc.

**Realização do processo de Extração de fonte de dados não eletrônicos**

Sem dúvidas é o processo mais trabalhoso, pois será necessário fazer a transformação do dado manual em dado de armazenamento digital (eletrônico). A melhor solução é colocar esses dados em um banco de dados relacional. Para tal tarefa, é preciso:

- Criar um banco de dados relacional;
- Projeto de banco de dados relacional com as tabelas de destino, ou seja, modelo entidade relacionamento níveis Conceitual, lógico e físico;
- Implementação do modelo entidade relacionamento físico;
- População das tabelas.

**Exemplo de Extração de Fontes de dados não-eletrônica**

Vamos supor que você encontrou um documento em papel com os nomes de departamentos da empresa, ou seja, uma fonte de dados não eletrônica. Então, será necessário criar um banco de dados com uma tabela que possa armazenar os dados desses departamentos (código do departamento, nome do departamento e localização do departamento). Os comandos aqui demonstrados são do SGBD Oracle.

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674684234640-Rg2czIoirf.png)

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674684291341-KMoVfgEqkm.png)

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674684325060-kkUeIw2kPL.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

Pronto! Realizada a extração de dados manuais para um banco de dados relacional.

**Exemplo de inserção de vários dados não eletrônicos, com um único comando.**

Vamos supor que sua fonte de dados tenha vários dados que precisam/devem ser carregados de uma só vez:

**Sequência de Comandos**

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674684457802-niIFWga4qA.png)

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674684509143-Q8kLUyWChs.png)

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674684533647-5a4eyg7fnk.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

**Fonte de Dados Estruturados**

São os Dados localizados em Bancos de Dados Relacionais/Planilhas Eletrônicas, ou seja, dados que se encontram dentro de uma estrutura como tabela (linhas e colunas);

**Realização do processo de Extração de fonte de dados estruturados**

Quando a fonte de dados já está em um banco de dados relacional, às vezes só é necessário fazer a organização dos dados, criação de tabelas de destino e inserção dos registros com o uso de recursos, como tabelas auxiliares e views.

**Exemplo de Extração de Fontes de dados estruturados**

Diferentemente do exemplo de Extração de Fontes de dados não-eletrônica, não será necessário criar um banco de dados, pois já existe. Os comandos aqui demonstrados são do SGBD Oracle.

São necessários os seguintes passos:

- Defina as tabelas de origem de dados:
- Defina as tabelas de destino dos dados;
- Faça a cópia da estrutura e dos dados de tabela de origem para a tabela de destino;
- Execute os seguintes comandos;

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674684606084-OhRImoyG3D.png)

Caso a tabela de destino já exista, para fazer a constância do processo, será necessário fazer somente a cópia dos registros. Para tal, execute o seguinte comando:

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674684672678-7D1YA6ysGO.png)

Outra situação bem comum é precisar estipular condições para inserir os dados, ou seja, é necessário que os dados estejam dentro de padrões e/ou condições para que sejam de nosso interesse, além de precisarmos fazer essa operação com apenas um comando.

Por exemplo, não queremos inserir todos os dados de uma tabela, queremos apenas alguns registros. Para tal, execute essa sequência de comandos:

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674684728945-PN8fXb8mMA.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674684813685-RQULPAPgUs.png)

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674685441736-tsq9wq5MU5.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674685443907-6KjNeewJqo.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

Outra situação bem corriqueira, é querer inserir os dados em tabelas de destino diferentes. Essa separação de tabelas pode ser por conta de uso, ou de ambiente, ou de aplicação, etc. Para tal, use essa sequência de comandos:

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674685508588-ekQyg1DqNh.png)

**Fonte de Dados Semiestruturados**

São os Dados localizados em Arquivos (TXT,XML, E-Mail, arquivos de outros Sistemas ERP, MainFrame);

**Exemplo de extração de fonte de dados semiestruturados para banco de dados Relacional:**

Amostra de Arquivo .CSV

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674685605412-SZTcMLrtGh.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674685667412-nnFRUjK27b.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

**Execute essa sequência de comandos no SGBD Oracle**

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674685705877-Us2sJzuUSs.png)

**Exemplo de extração de fontes de dados estruturados para ferramenta de _BI_**

Vamos fazer a demonstração com a ferramenta _Power BI_. É uma ferramenta com ampla atuação no mercado, fabricada pela _Microsoft_ e com grande capacidade de integração com vários tipos de ferramentas, aplicações, sgbd´s e diversos tipos de fontes de dados.

Agora, clique em obter Dados (observe a imagem abaixo):

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674685722891-CwwORV0b2Y.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674685757518-fiRnQ0y6c0.png)

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674685778791-AuF1lqQhZX.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674685813293-a56xKj5Bg5.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

Escolha a sua fonte de dados estruturado, no exemplo uma base dados do MySQL, depois clique em ligar (observe a imagem abaixo)

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674685854011-kKapSLQoM2.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

Informe o nome ou endereço ip do servidor onde está a base de dados

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674686247225-i45OFPnPpy.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

Selecione a(s) tabela(s) e visualize os dados, que serão carregados. Clique no botão carregar:

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674686278173-jmEnIW7f5b.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

Clique em Dados e visualize os dados na ferramenta

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674686334192-wxua6jXWCd.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

**Exemplo de extração de fonte de dados estruturados – planilha eletrônica**

Clique em obter dados

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674686398126-DaLPBIBFGi.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

Escolha a opção de planilha eletrônica excel “importar dados de um livro do _Microsoft_ Excel”

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674686437466-Ppu4LsS5Mr.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

Escolha o nome do arquivo da sua planilha eletrônica

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674686471710-y8rCc0EBg6.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

Visualize os dados que serão carregados na ferramenta e clique em **carregar**

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674686520252-4N41hZXzSE.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

Clique em Dados e visualize-os carregados na ferramenta

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674686766157-dVbDWACqKb.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

**Conteúdo bônus**

**Tópicos avançados**

Criando Visões (Views)

**Sintaxe:**

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674686820759-5JlXuu5dYo.png)

onde:

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674686858058-5pJUMZ7j3P.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

Há duas classificações para views: simples e complexa:

Uma **view simples**:

- Seleciona dados a partir de somente uma tabela.
- Não contém funções ou grupos de dados.
- Pode-se executar a DML.

Uma **view complexa**:

- Seleciona dados a partir de várias tabelas
- Contém funções ou grupos de dados
- Nem sempre pode-se executa a DML

**Exemplo 1:** Criar uma view com nome EMPVU10, que contenha detalhes tais como: número, nome e cargo dos funcionários que trabalham no departamento 10.

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674686898592-lChIOHx0yD.png)

**Exemplo 3:**  Criar uma view para exibir o nome do departamento e o menor salário, maior salário e a média salarial de cada departamento.

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674686924198-vEI41iThrr.png)

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674686962749-r63tWe4pbS.png)

No exemplo anterior, estava sendo criada uma view complexa para exibir os nomes de departamento, maior salário, menor salário e o salário médio por departamento. Note que os nomes alternativos foram especificados para a view. Esse é um requisito se uma coluna da view derivar de uma função ou expressão.

**1º Passo) Selecionando as fontes dos dados no ambiente OLTP**

Nossas fontes de dados são 2 tabelas (Empregados e Departamentos), que encontram-se no ambiente OLTP.

Nesse exemplo, o ambiente OLTP será um banco de dados relacional instalado no SGBD Oracle 11g versão Express Edition. Essa versão é distribuída no site do Oracle, de forma gratuita. Além disso, essa versão é própria para o uso acadêmico, sendo mais leve e muito fácil de instalar (processo next,next, finish). No link [http://www.oracle.com/technetwork/database/database-technologies/express-edition/downloads/index.html](http://www.oracle.com/technetwork/database/database-technologies/express-edition/downloads/index.html), você pode efetuar o download  das distribuições de 32 ou 64 bit, de acordo com a sua infraestrutura.

Depois de instalado o SGBD, é necessário executar os seguintes passos:

- Se conecte no banco de dados com o usuário SYS

          SQL> Conn sys/senha as sysdba

- Execute o script do usuário Scott , para criar as tabelas EMP e DEPT

          SQL> @ c:\diretório do oraclehome\rdbms\admin\scott.sql

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674687007572-dObTT0ihkg.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

- altere a senha do usuário Scott, sendo que a senha padrão é Tiger

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674687285218-dg0ZnlVUyT.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674687336174-vZ8dIRLhFG.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

- visualização dos dados da tabela emp

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674687415574-xACVrUVA2v.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

Visualização dos dados da tabela dept

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674687472172-LqMk8NMn2n.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

As tabelas dept e emp estão relacionadas na cardinalidade 1:N, onde na tabela dept a coluna deptno é a chave primária e na tabela emp a coluna deptno é a chave estrangeira, ainda na tabela emp a coluna empno é a chave primária.

Outro usuário importante para os nossos exemplos é o Schema do HR, que já vem criado por default. Portanto, basta definir a senha e liberar a conta deste usuário.

As tabelas desse usuário são: employees (dados do empregados) e departments  (dados do departamento).

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674687725407-PEvUvHzjxg.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

- visualização dos dados da tabela employees

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674687746288-y0ov3N3jPF.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

- visualização dos dados da tabela departments

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674687787190-5kg739DVyI.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

Pronto, seu ambiente OLTP está montado. Essas serão as fontes de dados que vamos trabalhar nos próximos passos.

**2º Passo) Definição de quais são relevantes para a estratégia do DW e geração de relatórios.**

Na tabela de employees do schema HR (empregados) temos os seguintes campos:

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674687862076-pn751CTSMN.png)

Na tabela departments (departamentos) temos os seguintes dados:

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674687896149-dQ8B5YxKdJ.png)

Depois de analisarmos a estrutura das nossas fontes de dados, é necessário selecionar nesse grupo de dados quais são relevantes para o DW, ou seja, quais dados serão utilizados para serem gerados os relatórios e as estatísticas para tomada de decisão.

Nesse exemplo, nossa escolha de dados relevantes são: código do funcionário, sobrenome do funcionário, salário, data de admissão, código do departamento e nome do departamento.

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674687937624-OgzFp9vGc7.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

**3º Passo) Montagem da Staging Area – Extração e Transformação dos dados**

Nunca devemos alterar os dados do ambiente OLTP. Para fazer a extração de dados, podemos criar outro banco de dados, outro tablespace, mas para levar os dados podemos utilizar o recurso de  uma view que tem como tabelas-base empregados e departamentos, conforme o comando abaixo:

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674687979908-rYXdkM3QfO.png)

É neste momento que se necessário também se realiza a transformação de dados.

Figura: Seleção dos dados da view staging_area

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674688005227-DqFL1x0iPA.png "Fonte: Autoral, 2022.")

Fonte: Autoral, 2022.

**4º Passo) Preparação do ambiente OLAP – Tabela destino**

Para se fazer a carga de dados, todos os objetos do ambiente do DW devem estar criados e preparados, conforme se vê no comando abaixo.

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674688054537-YBTuPd6g5v.png)

**5º Passo) Realização da Carga de dados**

Na realização da carga de dados, precisamos adequar os tipos dos dados, os nomes dos campos entre origem (Staging Area) e destino (Tabela do DW),  a ordem em que os dados estão dispostos na origem e como os campos serão disponibilizados no destino. No comando abaixo, podemos verificar a realização da carga:

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674688087637-41ccjfOkFA.png)

**6º Passo) Ajustando a Surrogate Key**

É necessário criar uma chave primária “falsa”, para identificar o registro no ambiente de DW, por esse motivo precisamos ajustar a SK na tabela, conforme comandos abaixo:

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674688123192-hTYiw2v2Hc.png)

**7º Passo) Visualização dos Dados e Geração de Relatórios**

Relatório de todos os empregados e seus respectivos departamentos:

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674688164935-6fEYQfbYfJ.png)

Relatório de todos os empregados e seus respectivos departamentos

![Fonte: Elaborado pelo autor, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674688202279-0CDtbKe41p.png "Fonte: Elaborado pelo autor, 2022.")

Fonte: Elaborado pelo autor, 2022.

Relatório da Soma Salarial e total de empregados por departamento

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674688237444-DvZuFUDOxg.png)

Relatório da Soma Salarial e total de empregados por departamento

![Fonte: Elaborado pelo autor, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674688259118-43UVNpQJ3R.png "Fonte: Elaborado pelo autor, 2022.")

Fonte: Elaborado pelo autor, 2022.

Relatório de custos por departamento e subtotal

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674688302355-KPrMQOii06.png)

Relatório de custos por departamento e subtotal

![Fonte: Elaborado pelo autor, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674688328296-AOIuudMF3o.png "Fonte: Elaborado pelo autor, 2022.")

Fonte: Elaborado pelo autor, 2022.

Para cada comando e/ou relatório, você pode criar uma procedure como o exemplo da figura acima, com o objetivo de agilizar o processo.


Referência Bibliográfica

ARAÚJO, Erika Maria Teixeira; BATISTA, Mônica de Lourdes Souza;  **Qualidade na Modelagem dos Dados de um Data Warehouse**; Disponível em: < [http://www.devmedia.com.br/qualidade-na-modelagem-dos-dados-de-um-data-warehouse/6978](http://www.devmedia.com.br/qualidade-na-modelagem-dos-dados-de-um-data-warehouse/6978) >.  Acesso em 20/12/2022

BARBIERI, Carlos. Bi : **Business Intelligence - Inteligência de Negócio: modelagem '&' tecnologia.** Rio de Janeiro: Axcel Books do Brasil, 2001. 424.

ELIAS, Diego; **Entendendo o processo de ETL.** 11 de Junho de 2014. Disponível em: < [https://canaltech.com.br/business-intelligence/entendendo-o-processo-de-etl-22850](https://canaltech.com.br/business-intelligence/entendendo-o-processo-de-etl-22850) >.  Acesso em 20/12/2022

GUEDES, Anselmo; **SERIA A MODELAGEM DIMENSIONAL UMA “BALA DE PRATA"?** Disponível em: < [https://imasters.com.br/banco-de-dados/seria-a-modelagem-dimensional-uma-bala-de-prata](https://imasters.com.br/banco-de-dados/seria-a-modelagem-dimensional-uma-bala-de-prata) > Acesso em 21/12/2022

JAMIL, George Leal. **Aspectos do ambiente gerencial e seus impactos no uso dos sistemas de inteligência competitiva para processos decisórios. Perspectivas em Ciência da Dados**. Belo Horizonte, v. 6, n. 2, p. 261-274, jul./dez. 2001.

KRATZ, L.G., et al. **Data Warehouse: a experiência da ANVISA.** Disponível em: <[https://www.researchgate.net/publication/228548408_Data_warehouse_a_experiencia_da_ANVISA](https://www.researchgate.net/publication/228548408_Data_warehouse_a_experiencia_da_ANVISA)>. Acesso em 20/12/2022

PRIMAK, Fábio Vinícius. **Extract, Transformation and Load (ETL)** - Ferramentas BI; 2015. Disponível em: [https://www.devmedia.com.br/extract-transformation-and-load-etl-ferramentas-bi/24408](https://www.devmedia.com.br/extract-transformation-and-load-etl-ferramentas-bi/24408) >. Acesso em 20/12/2022

RIBEIRO, Viviane; **O que é  ETL?** Disponível em: < [https://vivianeribeiro1.wordpress.com/2011/06/28/o-que-e-etl-2/](https://vivianeribeiro1.wordpress.com/2011/06/28/o-que-e-etl-2/) >. Acesso em 20/12/2022

SERRA, Laércio. **A essência do Business Intelligence - Inteligência de Negócio**. São Paulo: Berkeley, 2002. 288 p.

SHIMIZU, Tamio. **Decisão nas organizações: introdução aos problemas de decisão encontrados nas organizações e nos sistemas de apoio à decisão**. São Paulo: Atlas, 2001. 317 p. ISBN 8522427496.


## Validação e Consistência da Coleta de Dados

**Introdução**

Analisar o processo de coleta de dados para garantir que os dados coletados sejam válidos, consistentes, verídicos e, definir local de armazenamento de dados coletados.

**Resumo**

O procedimento de coleta de dados passa pelos seguintes passos:

- Identificar as fontes de dados;
- Conhecer a localização das fontes de dados;
- Conhecer a arquitetura tecnológica, onde essas fontes de dados estão armazenadas;
- Determinar como será o processo de extração de dados;
- Criar o local do destino desses dados;
- Realizar a efetiva extração de dados do local de origem para o local do destino;
- Automatizar e schedular todo o processo de extração (sempre que possível).

Depois que esses passos são realizados é necessário verificar se foram realizados corretamente. Com os dados extraídos, é preciso fazer a validação desses dados, ou seja, garantir que os dados obtidos são corretos, válidos, coerentes, íntegros e verídicos.

Determinar um formato e criar regras para importar os dados no formato padronizado. Por exemplo: trabalhando com datas o formato deve ser 99/99/9999. Deve-se garantir que todas as datas estejam nesse formato.

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674739194987-Q6mgmtC2Ie.png "Fonte: Autoral, 2022.")

Outro exemplo: trabalhando com valores monetários, garantir que os valores monetários tenham sempre duas casas decimais e o símbolo da moeda R$9.999,99.

```SQL
select salary, to_char(salary,'L999,999,999.99') from employees;
```

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674739230227-V9lbCFwtis.png "Fonte: Autoral, 2022.")

Quanto à consistência dos dados, por exemplo, em um campo salário, só podemos encontrar valores numéricos. Para tal criar funções que encontrem dados diferentes de números.

Quanto à veracidade dos dados, um exemplo clássico é o CPF, que possui os dois últimos dígitos verificadores que são obtidos através de uma fórmula matemática. Criar algoritmos, por exemplo, que validem os dados do cpf. Outro recurso também é validar os dados com bases governamentais, como a base de dados do DETRAN (departamento de trânsito de São Paulo).

![[Pasted image 20250417080016.png]]

Para garantir a integridade dos dados, pode-se usar as regras de negócio, por exemplo, vamos supor que no negócio exista uma regra que nenhum funcionário possa ter salário inferior a R$ 1.300,00. Então, no momento da extração, caso seja realizada a tentativa de inserir um valor que não respeite a regra imposta, ocorrerá um erro no processo de extração. Nesse último exemplo, podemos utilizar a constraint (restrição) de check (verificação) para impor regras de negócio.

![[Pasted image 20250417080147.png]]

**Staging Area**

Depois de validar os dados, essa extração leva os dados para uma área de trabalho chamada de área de staging. Essa área é dedicada para que se possa trabalhar e aplicar técnicas aos dados coletados.

A fase de coleta de dados pode ser entendida como a etapa onde os dados são extraídos dos OLTPs e conduzidos para a staging area (área de transição ou área temporária), em que são convertidos para um padrão específico. A conversão se faz essencial devido à diversidade existente nos dados originados desses sistemas, sendo fundamental a formação antecipada para o tratamento adequado.

Geralmente, um Banco de Dados específico para esse fim ou um tablespace, para armazenar os Dados que foram coletados das Fontes de Dados. 

Essa área também pode ser usada em outros processos, por exemplo, procedimento de backup (pois contém Dados de todas as Fontes), recuperação de dados (caso haja algum defeito nos Dados no Data Warehouse, pode fazer a recuperação a partir dos Dados que se acham na Staging Area), investigação (é possível apurar as cargas de Dados que foram executados, por meio do histórico ) e rastreabilidade (possibilita a investigação de adversidades no processo ETL) . 

Por executar todas essas funções, é essencial que a Staging Area seja construída na realização do processo de ETL, conforme se observa na Figura abaixo:

![[Pasted image 20250417080528.png]]

****Processo de recuperação:** caso haja um erro nas últimas 200 linhas de um carga de 20 milhões que foi executada no Data Warehouse, não é preciso desfazer toda a carga, pois as 200 linhas corretas estão na Staging Area. 

**Processo de Backup:** com a Staging Area é gerado um backup de todas as fontes de dados.

**Processo de Auditoria:** Por ter um armazenamento histórico dos dados, é possível verificar qual foi a carga de dados realizada no último mês, por exemplo.

**Processo de Rastreabilidade**: Como a Staging Area vai receber todos os dados, é possível investigar que tipo de processo está apresentando algum tipo de problema.**

==Chuck Ballard, Daniel M. Farrell, Amit Gupta, Carlos Mazuela, Stanislav Vohnik; Dimensional Modeling: In a Business Intelligence Environment; An IBM Redbooks publication;2012==

Nesta publicação IBM Redbooks, descreve-se os métodos de modelagem de dados dimensionais, especificamente concentrados em business intelligence – inteligência de negócio e data warehouse. Compreender como projetar, manter e usar um modelo dimensional para data warehouse que pode fornecer acesso e performance de dados necessários para a inteligência de negócios.

A inteligência de negócios é formada por uma arquitetura de data warehouse e um ambiente de consulta, análise e geração de relatórios. Aqui concentra-se na infraestrutura de data warehousing. Contudo, apenas um elemento específico, o modelo de dados, é considerado o princípio básico de desenvolvimento do data warehouse. Ou, mais precisamente, o tema da modelagem de dados e seu efeito nas aplicações comerciais e de organizações corporativas. O foco não é fornecer um tratado sobre métodos de modelagem dimensional, mas atingir um grau mais prático. Existe conteúdo técnico para projetar e manter esse ambiente, mas também conteúdo comercial.

Por exemplo, são usados estudos de caso para demonstrar como a modelagem dimensional pode afetar as exigências de business intelligence para suas tentativas de negócios. Além disso, é oferecida uma discussão detalhada sobre os fundamentos da consulta de Business Inteligence – Inteligência de negócio e modelagem de dados. Por exemplo, é apresentada a otimização de consulta e como se pode definir o desempenho do modelo de dados antes da implantação.

https://www.redbooks.ibm.com/redbooks/pdfs/sg247138.pdf

____
### Transformação de Dados
#### Integração de Dados

Dados que estão em um ambiente (por exemplo, o código do fornecedor embutido na região) e que deverão ser codificados a fim de facilitar o seu uso, associando-se a ele uma informação sobre a região.

![[Pasted image 20250422085555.png]]

#### Condensação de Dados
define a forma de se reduzir volumes de dados visando obter informação resumidas e sumarizadas.

![[Pasted image 20250422085655.png]]

![[Pasted image 20250422085831.png]]

#### Conversão de Dados
Define os procedimentos para se transformar dados em unidades, formatos e dimensões diferentes.

![[Pasted image 20250422090050.png]]

-----

## Localização e Tratamento de Dados Sujos

Conhecer e entender a Fase de Transformação de Dados; entender, descobrir e reconhecer os dados "sujos" e quais são seus malefícios para a descoberta do conhecimento.

**Resumo**

**Processo ETL – Extração, Transformação e Carga – Fase de Transformação**

Nessa etapa, a preocupação está voltada para a definição dos processos requeridos de transformação do modelo fonte para o modelo dimensional. As principais atividades de transformação são: limpeza dos dados, garantir a qualidade dos dados _(_Data Quality), descarte dos dados inválidos e a padronização.

Nesse ponto, os conceitos de extração dos dados e de seu tratamento podem ser divididos em: 

- **Filtro de Dados:** relaciona os procedimentos e condições para se eliminar os elementos de dados indesejáveis no modelo dimensional. Por exemplo, deseja-se que somente ordens de compras com valores totais maiores que R$1.000,00 sejam consideradas no sistema gerencial em projeto.
- **Integração de Dados**: define a forma de se relacionar informações existentes em fontes distintas e que deverão ser integradas no sistema gerencial. A integração dessas informações se torna fundamental para os requisitos do sistema e deverá ser previsto nessa fase. Como exemplo, poderia ser o caso de dados que estão codificados em um ambiente (por exemplo, o código do fornecedor embute região) e que deverão ser codificados, a fim de facilitar o seu uso, associando-se a ele uma informação explícita sobre região.
- **Condensação de Dados**: Define a forma de se reduzir volumes de dados visando obter informações resumidas. Como exemplo, podemos ter a sumarização em termos semanais de dados diários de vendas, ou o resumo em níveis geográficos, por exemplo, vendas por região.
- **Conversão de Dados:** define os procedimentos para se transformar dados em unidades, formatos e dimensões diferentes.
- **Derivação de Dados**: define os meios e fórmulas para de produzir dados virtuais, a partir de dados existentes.

Figura 1: Obtenção dos dados

![Fonte: BARBIERI, 2001](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674740704140-n49M4AECFz.png "Fonte: BARBIERI, 2001")

Fonte: BARBIERI, 2001

**Processo de Limpeza dos dados**

Garantir as propriedades das colunas, as estruturas de dados, dados preenchidos e regras dos dados. Além de garantir regras de negócio e armazenar o dado  limpo.

Alguns exemplos de problemas com os dados fontes que precisam de limpeza:

- Colunas que F[altam valores](https://sigaosnumeros.wordpress.com/sumario/descomplicando-os-dados/como-encontrar-dados/criando-sua-base-de-dados/ed-guia-de-limpeza-de-dados/#faltamvalores);
- [Zeros substituem os valores que faltam](https://sigaosnumeros.wordpress.com/sumario/descomplicando-os-dados/como-encontrar-dados/criando-sua-base-de-dados/ed-guia-de-limpeza-de-dados/#zerossubstituem);
- [Faltam dados que você sabe que deveriam estar ali](https://sigaosnumeros.wordpress.com/sumario/descomplicando-os-dados/como-encontrar-dados/criando-sua-base-de-dados/ed-guia-de-limpeza-de-dados/#faltamdados);
- [Linhas ou valores estão duplicados](https://sigaosnumeros.wordpress.com/sumario/descomplicando-os-dados/como-encontrar-dados/criando-sua-base-de-dados/ed-guia-de-limpeza-de-dados/#linhasouvalores);
- [Formatos de datas estão inconsistentes](https://sigaosnumeros.wordpress.com/sumario/descomplicando-os-dados/como-encontrar-dados/criando-sua-base-de-dados/ed-guia-de-limpeza-de-dados/#formatodedatas);
- [Unidades não estão especificadas](https://sigaosnumeros.wordpress.com/sumario/descomplicando-os-dados/como-encontrar-dados/criando-sua-base-de-dados/ed-guia-de-limpeza-de-dados/#unidades);
- [Nomes de campos estão ambíguos](https://sigaosnumeros.wordpress.com/sumario/descomplicando-os-dados/como-encontrar-dados/criando-sua-base-de-dados/ed-guia-de-limpeza-de-dados/#nomesdecampos);
- [Números foram guardados como texto](https://sigaosnumeros.wordpress.com/sumario/descomplicando-os-dados/como-encontrar-dados/criando-sua-base-de-dados/ed-guia-de-limpeza-de-dados/#numerostexto).

**Processo de Qualidade dos dados**

Dados corretos com nomes e descrições, não podem ser ambíguos, todos os dados devem ser únicos. Além disso, devem ser consistentes de acordo com as regras definidas e, por fim, os dados devem ser completos, por exemplo, endereço.

Exemplos de Dados com qualidade:  A inexistência de dados duplicados, o conhecimento do número exato de clientes, a obtenção de uma visão única de cliente ou a segmentação de clientes.

**Processo de padronização dos dados**

Padronizar os dados da coluna das dimensões, padronizar/garantir regras de indicadores, além de garantir as regras de negócio para as colunas e padronizar métricas e tipos de dados.

Um exemplo de dado padronizado, no item regra de negócio: suponha que na empresa nenhum funcionário possa ganhar menos de 1 salário mínimo. Se os dados de salário estiverem padronizados, não se deve encontrar nenhum salário nulo ou inferior ao salário mínimo estabelecido. É importante ressaltar que, embora a regra de negócio se refira ao salário, não é possível fazer a padronização na coluna salário sem verificar e padronizar a coluna data de pagamento.

**Staging Area II**

Embora não seja obrigatória, recomenda-se fortemente que esta área seja criada, pois é o local onde todos os dados já estão limpos, tratados e padronizados. Neste momento, todos os dados estão prontos para se fazer a carga no DW.

**Visão Geral sobre Modelagem Dimensional de Dados**

A estrutura dimensional modifica a ordem de distribuição de campos por entre as tabelas, permitindo uma formatação estrutural mais voltada para os muitos pontos de entradas específicos (as chamadas dimensões) e menos para os dados granulares em si (os chamados fatos). Isso significa que numa estrutura dimensional os dados estarão numa forma quase estelar, onde várias tabelas de entradas estarão se relacionando com algumas (poucas) tabelas de informações, criando uma notação mais sintética, legível e objetiva.

O modelo dimensional oferece clara e diretamente os elementos que precisam para buscar as informações sobre fatos via dimensões de referências, diferindo da malha relacional, ou de rede, próprias dos modelos anteriores, em que não existem estruturas específicas de entrada. 

A modelagem dimensional é a técnica utilizada para se ter uma visão multidimensional dos dados.

O DW é representado por um modelo multidimensional de dados, apresentando as informações na forma de cubos de dados.

A modelagem é utilizada para sumarizar e reestruturar os dados e apresentá-los em visões que suportem a análise de seus valores.

O modelo multidimensional possui três elementos básicos: fatos, dimensão e medidas.

Ao elaborar o modelo dimensional, o foco deve ser nos requisitos e objetivos do negócio, não na tecnologia e nos dados. O envolvimento do patrocinador e usuários gerenciais é essencial para o sucesso. Adote uma abordagem incremental e iterativa para o desenvolvimento do DW. O desempenho das consultas do usuário e a facilidade de uso são os fatores mais críticos. Apresente os dados de forma simples, e com a semântica clara. O nível de detalhe deve chegar até os dados atômicos. Desenvolva o modelo dimensional com as visões Conceitual, lógica e Física.

____

==rastrear dados: pode ser dado um "count", para que saibamos quantos campos diferentes existem, no caso de um CPF que não existem 2 iguais no mundo real responder com dar um número inferior a um ID por exemplo==

----

## Fase T- Transformação/limpeza de Dados

**Introdução**

Definir padrões para os dados coletados. Eliminar todos os dados inconsistentes. Fazer as etapas de conversão, condensação e adequação dos dados. Conhecer e aplicar os processos para transformar e limpar os dados.

**Exemplo de Padronização de Dados**

Trata-se de um pequeno arquivo no formato .csv, com 3 campos, o código do cliente, o nome do cliente e o campo sexo. Observe os dados do campo sexo. Perceba que não há padrão. Abaixo é apresentada a seguinte fonte de Dados.

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1675262377369-0EPWZIQnJ7.png)

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1675262522946-fgAB8tiwV5.png)

# Processo de Padronização de Dados

#### 1. Criação da Staging Area

Execute os seguintes comandos no SGBD Oracle para criar o diretório de armazenamento:

```SQL
CREATE OR REPLACE DIRECTORY descomplica_dir AS 'c:\descomplica';
GRANT READ, WRITE ON DIRECTORY descomplica_dir TO hr;
```

#### 2. Criação da Tabela Externa

Crie uma tabela externa para receber os dados a serem padronizados:

```SQL
CREATE TABLE sexo_externa
(
    ID varchar2(3),
    NOME varchar2(50),  
    sexo varchar2(10)
)
ORGANIZATION EXTERNAL
(
    TYPE ORACLE_LOADER
    DEFAULT DIRECTORY FAM_DIR
    ACCESS PARAMETERS
    (
        RECORDS DELIMITED BY NEWLINE
        FIELDS TERMINATED BY ','
    )
    LOCATION ('sexo.csv')
);
```

#### 3. Transformação dos Dados

Crie e consulte a tabela de transformação:

```SQL
CREATE TABLE sexo_transformacao AS (SELECT * FROM sexo_externa);
SELECT * FROM sexo_transformacao;
```

#### 4. Identificação de Variações

Identifique todas as variações no campo sexo:

```SQL
SELECT DISTINCT sexo FROM sexo_transformacao ORDER BY sexo;
```

#### 5. Aplicação do Padrão

Atualize os valores para o padrão estabelecido:

```SQL
-- Padronização para 'F'
UPDATE sexo_transformacao
SET sexo = 'F'
WHERE sexo IN (' Fem', ' Feminino', ' mulher', 'f', 'Fem', 'Feminino');

-- Padronização para 'M'
UPDATE sexo_transformacao
SET sexo = 'M'
WHERE sexo IN ('H', 'h', 'homem', 'm', 'Masc', 'Masculino', 'masculino');
```

#### 6. Verificação da Padronização

Verifique se os dados estão padronizados:

```SQL
SELECT * FROM sexo_transformacao;
SELECT DISTINCT sexo FROM sexo_transformacao ORDER BY sexo;

-- Contagem por sexo
SELECT sexo, COUNT(sexo)
FROM sexo_transformacao
GROUP BY ROLLUP(sexo);
```

_____
# Processo de Eliminação de Dados Duplicados

## 1. Preparação do Ambiente

```SQL
CONN system/oracle
CREATE USER dup IDENTIFIED BY dup ACCOUNT UNLOCK;
GRANT DBA TO dup;
CONN dup/dup
```

#### 2. Criação da Tabela e Inserção de Dados

```SQL
CREATE TABLE cliente(
    cod_cli NUMBER(3) PRIMARY KEY,
    nome_cli VARCHAR2(30),
    cpf VARCHAR2(11)
);

CREATE SEQUENCE cod_cli;

INSERT INTO cliente VALUES (cod_cli.NEXTVAL, 'JOSE DA SILVA', '12345678901');
INSERT INTO cliente VALUES (cod_cli.NEXTVAL, 'MARIA DE JESUS', '12345678912');
INSERT INTO cliente VALUES (cod_cli.NEXTVAL, 'JOAO ANTONIO', '12345678901');
COMMIT;
```

#### 3. Identificação de Duplicados

```SQL
SELECT COUNT(*) FROM cliente;
SELECT COUNT(cpf), cpf FROM cliente GROUP BY cpf;
SELECT * FROM cliente WHERE cpf = '12345678901';
```

#### 4. Eliminação de Duplicados

```SQL
DELETE FROM cliente WHERE cod_cli = 3;
```

#### 5. Verificação

```SQL
SELECT COUNT(*) FROM cliente;
SELECT COUNT(cpf), cpf FROM cliente GROUP BY cpf;
```

----

## Processo de Tratamento de Dados Nulos

#### 1. Preparação do Ambiente

```SQL
CONN system/oracle
DROP USER dup CASCADE;
CREATE USER dup IDENTIFIED BY dup ACCOUNT UNLOCK;
GRANT DBA TO dup;
CONN dup/dup
```

#### 2. Criação e População da Tabela

```SQL
CREATE TABLE cliente(
    cod_cli NUMBER(3) PRIMARY KEY,
    nome_cli VARCHAR2(30),
    cpf VARCHAR2(11)
);

CREATE SEQUENCE cod_cli;

INSERT INTO cliente VALUES (cod_cli.NEXTVAL, 'JOSE DA SILVA', '12345678901');
INSERT INTO cliente VALUES (cod_cli.NEXTVAL, 'MARIA DE JESUS', '12345678912');
INSERT INTO cliente VALUES (cod_cli.NEXTVAL, 'JOAO ANTONIO', NULL);
INSERT INTO cliente VALUES (cod_cli.NEXTVAL, 'ELIZABETH ALMEIDA', NULL);
COMMIT;
```

#### 3. Identificação de Nulos

```SQL
SELECT COUNT(*), cpf FROM cliente GROUP BY cpf;
SELECT * FROM cliente WHERE cpf IS NULL;
```

#### 4. Tratamento de Nulos

```SQL
-- Eliminação
DELETE FROM cliente WHERE cod_cli = 3;

-- Atualização
UPDATE cliente SET cpf = '12345678913' WHERE cod_cli = 4;
```

#### 5. Verificação

```SQL
SELECT COUNT(*), cpf FROM cliente GROUP BY cpf;
SELECT * FROM cliente WHERE cpf IS NULL;
```

-----

## Processo de Tratamento de Redundâncias

#### 1. Preparação do Ambiente

```SQL
CONN system/oracle
DROP USER dup CASCADE;
CREATE USER dup IDENTIFIED BY dup ACCOUNT UNLOCK;
GRANT DBA TO dup;
CONN dup/dup
```

#### 2. Criação das Tabelas

```SQL
CREATE TABLE paciente (
    cod_pac NUMBER(4) PRIMARY KEY,
    cod_pessoa NUMBER(4)
);

-- População
INSERT INTO paciente VALUES (1234, 4);
INSERT INTO paciente VALUES (1231, 5);
INSERT INTO paciente VALUES (1232, 1);
COMMIT;

CREATE TABLE pessoa (
    cod_pessoa NUMBER(4) PRIMARY KEY,
    endereco VARCHAR2(30),
    nome VARCHAR2(30),
    data_nasc DATE
);

-- População
INSERT INTO pessoa VALUES (1, 'r.x,100', 'jose DA SILVA', '01/01/01');
INSERT INTO pessoa VALUES (2, 'r.y,100', 'joao ANTONIO', '01/02/01');
INSERT INTO pessoa VALUES (3, 'r.z,100', 'maria DE JESUS', '10/04/03');
INSERT INTO pessoa VALUES (4, 'r.w,100', 'antonio CARLOS', '01/05/02');
INSERT INTO pessoa VALUES (5, 'r.x,200', 'joaquim CRUZ', '11/10/04');

CREATE TABLE medico (
    crm NUMBER(5) PRIMARY KEY,
    cod_pessoa NUMBER(4)
);

-- População
INSERT INTO medico VALUES (12345, 1);
INSERT INTO medico VALUES (23451, 2);
INSERT INTO medico VALUES (23452, 3);
COMMIT;
```

#### 3. Identificação de Redundância

```SQL
-- Tabela de médicos
CREATE TABLE medico_r AS 
SELECT m.crm crm, p.nome nome_medico, p.endereco "endereco do medico", p.data_nasc "dt_nascimento"
FROM pessoa p JOIN medico m ON (p.cod_pessoa = m.cod_pessoa);

-- Tabela de pacientes
CREATE TABLE paciente_r AS 
SELECT pa.cod_pac codigo_paciente, p.nome nome_paciente, p.endereco "endereco do paciente", p.data_nasc "dt_nascimento"
FROM pessoa p JOIN paciente pa ON (p.cod_pessoa = pa.cod_pessoa);
```

#### 4. Eliminação de Redundância

Utilizando a técnica de generalização/especialização:

```SQL
-- Consulta de médicos
SELECT m.crm crm, p.nome nome_medico, p.endereco "endereco do medico", p.data_nasc "dt_nascimento"
FROM pessoa p JOIN medico m ON (p.cod_pessoa = m.cod_pessoa);

-- Consulta de pacientes
SELECT pa.cod_pac codigo_paciente, p.nome nome_paciente, p.endereco "endereco do paciente", p.data_nasc "dt_nascimento"
FROM pessoa p JOIN paciente pa ON (p.cod_pessoa = pa.cod_pessoa);

-- Identificação de redundância
SELECT p.nome nome_medico, m.crm crm_medico, p.nome nome_paciente, pa.cod_pac codigo_paciente
FROM pessoa p 
JOIN medico m ON (p.cod_pessoa = m.cod_pessoa)
JOIN paciente pa ON (p.cod_pessoa = pa.cod_pessoa);
```

#### 5. Verificação

```SQL
SELECT * FROM pessoa;
SELECT * FROM paciente;
SELECT * FROM medico;
```

**Processo de Transformação ou Data Quality**

Para iniciar o procedimento de transformação, a Staging Area deve possuir os dados que foram coletados das fontes de dados, que podem demonstrar uma diversidade enorme de defeitos. São eles: 

- Ausência de Valores (nulos) presentes onde não deveriam estar (por exemplo, no campo nome do cliente, toda pessoa tem nome, não deve ter nulo);
- Uso incorreto de valores padrão (por exemplo, campos que mostram algum tipo de status);
- Violação de integridade do domínio de dados (por exemplo, o padrão seria [F para feminino  e M para Masculino], mas encontram-se os valores f,F,m,M,fem,masc,1 e 2 );
- Violação de integridade do valor dos dados (por exemplo, um código que deve ser somente numérico, ter algum dado que apresenta letras);
- Violação de integridade referencial de dados (erros nos relacionamentos, por exemplo, o registro de pedido de um cliente não pode existir, a menos que o registro do cliente já exista);
- Armazenamento de campos calculados (por exemplo, não armazene o salário líquido e sim o salário bruto e os percentuais de desconto);
- Dados incorretos (por exemplo, o campo CEP preenchido com um valor errado, exemplo: 99999-999 ou ainda um número cadastrado dessa forma: CPF 000.000.000-00). 
- Registros redundantes e/ou campos redundantes (por exemplo, ter o nome, o endereço e o telefone do cliente registrado em duas tabelas diferentes). Vamos supor que o cliente também seja funcionário, se o projeto de banco de dados for ruim, haverá o registro desses dados na tabela de cliente e também na tabela de funcionários.
- Definição de máscaras e formatos para todos os dados que necessitam (por exemplo, os campos que armazenam datas devem ter um formato definido e padronizado DD/MM/YYYY e todas as datas devem ficar armazenadas e visualizadas no formato estabelecido). 
- Quando for um campo que armazena quantidades deve ter a unidade estabelecida e padronizada. (por exemplo, Kg, mt, KM, pc).
- Os tipos dos dados devem ser respeitados conforme o especificado (por exemplo, o número da nota fiscal deve ser armazenado em um campo do tipo numérico e não em um campo alfanumérico).
- Garantir o armazenamento dos dados corretos (por exemplo, todos os dados devem ter nomes, descrições, devem ser únicos e completos).

Na etapa de Transformação todos esses defeitos devem ser reparados e, quando não for possível fazer a reparação, os dados que tiverem esses defeitos devem ser excluídos, ou seja, deve-se garantir a consistência, integridade, respeitando as normas de negócio e qualidade dos dados. Por isso, essa fase do processo ETL também pode ser chamada de Data Quality, que significa atingir a qualidade de dados.  Somente com a qualidade de dados é possível executar uma consulta no Data Warehouse confiável e que realmente cumpra com sua função de sustentar a tomada de decisão estratégica.

Para reconhecer um dado com qualidade, ao analisar a massa de dados depois de passar por todo o procedimento de Transformação, não se deve achar dados duplicados. Outro indicador de qualidade é o conhecimento do número exato de clientes/produtos. 

Mais um indicador de um dado padronizado na regra de negócio: suponha que na empresa nenhum funcionário possa ganhar menos de 1 salário mínimo. Se os dados de salário estiverem padronizados, não se deve encontrar nenhum salário nulo ou inferior ao salário mínimo estabelecido. 

Fazer a preparação dos dados históricos para realizar a transformação dos dados, realização de cálculos entre os dados das colunas que sejam necessários, geração e utilização da surrogate key. 

No Data Warehouse, o objetivo é manter a integridade e criar as Surrogate Keys para não depender das chaves primárias que venham dos sistemas legados. Por exemplo, a chave do registro da tabela de clientes se chama ch_cliente. Para o registro do cliente 'Beth' a chave é "bet123ch554". É uma chave muito ruim de manipular, pois é alfanumérica. O objetivo é que a surrogate Key traga integridade e performance no acesso aos dados do Data Warehouse. Para tal, a Surrogate Key sempre deve ser numérica e sequencial. As Sk´s são aplicadas nas dimensões para estabelecer o relacionamento da tabela fato com as tabelas de dimensões, constantes no modelo dimensional. 

A criação da Staging Area II não é uma obrigatoriedade, mas ajuda muito na organização do processo, pois os dados constantes nessa área encontram-se limpos, tratados e padronizados. Isso significa que estão prontos para a próxima etapa chamada de carga no Data Warehouse.  Esta área acaba servindo como um “porto seguro “ dos dados, antes de realizar a carga.

## Data Quality

**Introdução**

Nesta aula, vamos definir o que é um ambiente com qualidade de dados. Também é importante saber como manter e receber novos dados com o mesmo padrão no formato, veracidade e consistência.

Os dados podem apresentar vários formatos, mas no processo de transformação de dados, ou seja, para fazer a limpeza dos dados, é importante que estejam no mesmo formato.

Podemos encontrar as datas armazenadas de várias formas. Observe a imagem abaixo:

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674831864120-Q6T5oOcCOE.png "Fonte: Autoral, 2022.")

Use a função to_date para padronizar todas as datas no mesmo formato, conforme o exemplo abaixo:

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674831875908-eXqrCw9B63.png "Fonte: Autoral, 2022.")

Observe que, embora os dados das datas tenham sido inseridos em formatos diferentes, o armazenamento do formato da data permanece o mesmo.

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674831894087-0IUifurrKL.png)

**Formatação de Dados Maiúsculas e Minúsculas**

Quando os dados não estão no mesmo padrão de letras maiúsculas ou minúsculas, podemos ter como resultado, relatórios com dados totalizadores inconsistentes, como se pode observar no exemplo abaixo.

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674831905992-o1MFMWm2Lf.png "Fonte: Autoral, 2022.")

No entanto, observe que existem 4 professores com o nome de “Jose”, mas como estão cadastrados com padrões de letras maiúsculas e minúsculas diferentes, o resultado da contagem mostra somente 1, ou seja, um relatório com dados totais inconsistentes.

Por esse motivo, é fundamental adotar um padrão e aplicar esse padrão aos dados armazenados no banco de dados. Conforme podemos observar no exemplo abaixo:

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674831922330-X8c1UDDm11.png "Fonte: Autoral, 2022.")

Observe que foi adotado um padrão de colocar todos os nomes dos professores em letra maiúscula. Isso foi feito, com o uso da função Upper, aplicada a todos os registros da tabela. Perceba que depois que os dados estão padronizados, os relatórios totalizadores fornecidos agora são consistentes, pois existem 4 professores com o nome de “José”.  Outras funções como lower (letras minúsculas) ou ainda initcap (primeira maiúscula e demais minúsculas), também podem ser utilizadas para adotar e aplicar padrões aos dados.

**Data Quality – Qualidade de Dados**

O Data Quality é o local onde temos a garantia que todos os dados já passaram pelo processo de transformação, estão limpos, padronizados e consistentes.

Para garantir que os dados tenham qualidade, consistência, padrão e, principalmente, que os novos dados cheguem ao banco de dados com essa mesma qualidade, é importante ajustar o projeto de banco de dados e aplicar restrições que permitam que dados errados sejam inseridos, conforme se observa nos exemplos abaixo:

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674831932532-EvBKGGVj5Y.png "Fonte: Autoral, 2022.")

Observe que a tabela foi construída sem a constraint de check. Isso significa que o campo sexo pode aceitar qualquer valor, o que é um erro, pois esse campo tem um domínio de valores.

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674831956704-uF2vsCYnbW.png "Fonte: Autoral, 2022.")

Verifique que, depois que a constraint de check foi aplicada ao campo sexo, os valores que não estão definidos na restrição não serão aceitos. Essa aplicação garante a padronização, a mesma formatação e a consistência de dados do campo sexo.

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674832017852-4ulsrOHNGe.png "Fonte: Autoral, 2022.")

Não podemos ter nulos em campos de nome, pois todas as pessoas têm nome. Com a adição da constraint de not null no campo nome_pessoa, não será permitida a inserção de dados nulos nesse campo, impondo a integridade dos dados desse campo.

**NÃO ARMAZENE CAMPOS CALCULADOS (INFORMAÇÃO)**

Campos calculados são informações e essas com o passar do tempo tornam-se velhas, ou seja, tornam-se falsas. Novamente, podendo gerar relatórios inconsistentes, conforme no exemplo abaixo:

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674832028483-VZTAvLeGo9.png "Fonte: Autoral, 2022.")

Note que quando armazenamos a idade de um aluno, somente com o passar do tempo a informação torna-se falsa, pois no próximo ano esse aluno já terá 26 anos. Se armazenarmos o dado que, neste exemplo, é a data de nascimento, podem se passar 1000 anos, mas conseguiremos chegar sempre à informação correta.

![Fonte: Autoral, 2022.](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1674832040249-H19o2aYsft.png "Fonte: Autoral, 2022.")

Veja que fazendo a operação de subtração com o dado data de nascimento, chegamos sempre a idade correta do aluno, por esse motivo, nunca armazene campos calculados, somente guarde dados, assim você mantém o seu data quality.

**Tópicos Avançados**

SANTOS, Ricardo Zonta; **Staging Area e ODS;** Disponível em: < [https://medium.com/@ricardozontasantos/staging-area-e-ods-c573c0d6477](https://medium.com/@ricardozontasantos/staging-area-e-ods-c573c0d6477) >. Acesso em 20/12/2022

Benefícios da Adoção de uma Camada ODS (Staging Area II):
- Dados unificados e padronizados de diferentes origens;
- Possibilidade de geração de relatórios mais elaborados, por conta das diferentes novas informações que podem ser agregadas e técnicas de armazenamento, como ‘snapshots’ (visões fotográficas);
- Independência processual da origem, evitando a concorrência com os recursos produtivos;

Por ser detalhado, o ODS é frequentemente relacionado à geração de relatórios e consultas tático-operacionais, embora não se restrinja a esse fim.

A camada ODS e a camada STG fazem parte da chamada **Camada de Integração,** responsável por estabilizar e dar utilidade ao dado da origem para ser consumido pela camada de Data Warehouse.

STG -Staging Area é a área de recepção dos dados de origem para consumo das camadas seguintes do Data Warehouse. Não mantém dados entre os ciclos de carga e não deve possuir transformações de dados.

ODS - Operational Data Store é uma camada de dados detalhados uniformizados que dão suporte às visões e relatórios tático-operacionais e podem ser utilizados como apoio às análises de BI e origem para construção de Data Warehouses.

Juntas a Staging Area e a ODS, formam a Camada de Integração de Dados.