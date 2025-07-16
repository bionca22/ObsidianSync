**Resumo**

Pandas é uma excelente biblioteca em _Python_ que lhe permite ter acesso a um arsenal de ferramentas para análise de dados. O nome é derivado do termo inglês "panel data"(dados em painel), um termo usado em estatística e econometria para conjunto de dados que incluem várias unidades amostrais (indivíduos, empresas, etc) acompanhadas ao longo do tempo.

Para instalação do pandas temos como pré-requisito a instalação do python, então, caso não tenha o python instalado na sua máquina siga os seguintes passos:

1- Acesse o site [www.python.org](http://www.python.org/)

2- Clique em download

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1667236012837-94mSsYInKX.png "Fonte: Autoral, 2022")

3- Baixe a versão atual para o seu sistema operacional.

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1667236269457-dBNVhzCgkt.png "Fonte: Autoral, 2022")

4- Após o download Clique no instalador

![Figura 3 - Criado por Fabricio Mattos](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1667236307836-P7oEnJBX1u.png "Figura 3 - Criado por Fabricio Mattos")

Figura 3 - Criado por Fabricio Mattos

Clique em instalar e marque a opção “Add Python to path” e deixe a instalação terminar.

Após a instalação ser finalizada abra o prompt de comando e digite python

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1667236688560-gA7EC7H7Xr.png "Fonte: Autoral, 2022")


Agora que tem o python instalado vamos instalar a IDE Pycharm

1- Acesse o site [www.jetbrains.com/pycharm/](http://www.jetbrains.com/pycharm/)

2- Clique em download

![Figura 5 - Criado por Fabricio Mattos](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1667236751467-3vlbL6KyBw.png "Figura 5 - Criado por Fabricio Mattos")

3- Faça o download da versão comunity do seu sistema operacional.

![Figura 6 - Criado por Fabricio Mattos](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1667236777008-5hbxYM2ZMZ.png "Figura 6 - Criado por Fabricio Mattos")

4- Após o download Clique no instalador e siga os passos

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1667236847127-PHitptxdc6.png "Fonte: Autoral, 2022")

5- Após a instalação procure por pycharm na barra de busca ou aplicativos

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1667236995326-lIvemX1qua.png "Fonte: Autoral, 2022")

Após abrir o Pycharm vamos configurar o interpretador python, pois é ele o responsável por entender o código python e executá-lo.

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1667237051426-pt7TXxTDzc.png "Fonte: Autoral, 2022")

Agora vamos instalar o Anaconda:

O Anaconda é uma plataforma open-source que contém diversas bibliotecas para uso na área de machine learning e data Science. Quando a instalamos já temos o  pandas, o numpy, matplotlib, scipy, jupyter dash e outras libs utilizadas para manipulação, tratamento e  analise de dados.

Vamos baixar o instalador do anaconda na página: [https://www.anaconda.com/products/distribution](https://www.anaconda.com/products/distribution)

Após feito o download, abra o instalador

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1667237127966-UaexqZNduz.png "Fonte: Autoral, 2022")

Para instalar clique no botão next e siga o passo a passo, não é necessário alterar nada, pois utilizaremos a instalação default

**Jupyter notebook**

O Jupyter Notebook é um aplicativo web para criar e compartilhar documentos. Ele é muito útil pois é possível escrever o código e analisar a saída dos dados.

Criando uma nova pasta:

Para criar uma nova pasta clique no botão new a direita acima e clique em folder:

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1667237163406-pPf6CXHh1R.png "Fonte: Autoral, 2022")


É possível renomear a pasta clicando nela e depois no botão rename:

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1667237181587-9xamtnKhOR.png "Fonte: Autoral, 2022")

Criando um notebook

Para criar um notebook clique no botão new a direita acima e clique em python 3:

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1667238043259-SoDd4NuX90.png "Fonte: Autoral, 2022")

**Dataframes**

O pandas foi criado para trabalhar com estruturas de dados de uma maneira fácil e rápida e essa estrutura é chamada de _DataFrame_, que podemos visualizar como sendo um estrutura bidimensional de linhas e colunas como se fosse uma planilha no excel.

Para criar um _dataframe_ podemos utilizar o comando:

pandas.DataFrame()

Vamos agora ver como podemos criar dataframe a partir de leitura de diversas estruturas de dados como csv, excel, html, parquet e muitos outros.

Para criar um dataframe a partir de um arquivo csv usamos o seguinte comando:

Pandas.read_csv(‘caminho/do/arquivo/arquivo.csv)

Além disso, o pandas aceita diversos parâmetros na hora de ler o arquivo, como por exemplo o separador, encoding e muitos outros.

Uma das funções muito utilizadas para analisar como estão distribuídos os dados é a função describe, com ela podemos ter diversas informações em um único comando conforme exemplo:

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1667238102460-8a8EwqULyg.png "Fonte: Autoral, 2022")

Podemos também utilizar API para acessar informação e transformá-la em Dataframes. Uma API muito usada é a yfinance, com ela é possível acessar informações do mercado financeiro. Para utilizar essa api primeiro precisamos instalá-la, podendo ser pelo terminal ou pela própria IDE, vejamos exemplo:

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1667238171359-QtbBQVWDyu.png "Fonte: Autoral, 2022")


Agora vamos buscar informações de um determinado ativo financeiro, por exemplo as ações da Petrobrás:

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1667238198061-ASZFVDj1lU.png "Fonte: Autoral, 2022")

Vejamos como ficou o dataframe:

![Fonte: Autoral, 2022](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1667238499561-RHYeMFni1M.png "Fonte: Autoral, 2022")


Repare que o _dataframe_ contém informação de 1 ano, pois foi passado um parâmetro informando a quantidade de dias que deveria ser retornado.

**Como aplicar na prática o que aprendeu**

Toda análise de dados deve antes passar por um processo de EDA (_Exploratory data Analisys_) ou em português análise exploratória de dados, onde se verifica como estão os dados que se deseja trabalhar. Com o EDA, é possível fazer uma investigação acerca dos dados para verificar padrões, distribuição dos dados com o comando _describe_, existência de dados nulos ou se os valores possuem _outliers._ É uma parte muito importante, pois para utilização dos dados, eles têm que ser confiáveis para gerar informações de valor.

**Conteúdo bônus**

**Tópicos avançados**

Para saber mais sobre a biblioteca que pode ser usada, vá até a página do gerenciador de pacotes do python chamada Pypi em [https://pypi.org/](https://pypi.org/).

Utilize a biblioteca _yfinan_ce para buscar informações de outras ações e utilize o comando _describ_e para analisar como está o preço de fechamento deste ativo.

Dicas:

1- Usando a IDE, instale a biblioteca _yfinance_;

2- Importe a biblioteca que acabou de instalar;

3- Pesquise pelo ativo desejado, faça uma busca no GOOGLE

4- A sigla da ação deve estar acompanhada sempre pelo sufixo .SA conforme exemplo.

5- Salve em um _dataframe_

6- Utilize a função _describe_

Caro estudante, você consegue acessar os códigos utilizados na disciplina no link a seguir: [https://github.com/FaculdadeDescomplica/StatisticsLibraryinPython](https://github.com/FaculdadeDescomplica/StatisticsLibraryinPython)