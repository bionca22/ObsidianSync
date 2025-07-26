
https://www.postgresql.org/docs/current/transaction-iso.html#XACT-READ-COMMITTED
#### JSONB
E possível utilizar o PostgreSQL de forma flexível, modelando dados de maneira que se assemelhe a um banco de dados NoSQL, como um banco de dados chave-valor ou um banco de dados orientado a documentos. 

##### Como modelar dados NoSQL no Supabase:
 O PostgreSQL possui um tipo de dado chamado `JSONB`, que permite armazenar dados semi-estruturados como JSON dentro de uma coluna de tabela. Isso pode ser usado para simular um banco de dados chave-valor ou um banco de dados orientado a documentos, onde cada registro pode ter um esquema diferente.

Em detalhes:

- **Formato:**
    O JSON é um formato baseado em texto que utiliza uma estrutura simples, inspirada na sintaxe de objetos JavaScript. 

- **Leitura:**
    É facilmente lido e compreendido por humanos, o que facilita a depuração e o entendimento dos dados. 

- **Independência de linguagem:**
    O JSON pode ser usado com qualquer linguagem de programação, o que o torna uma escolha ideal para a troca de dados entre diferentes sistemas. 

- **Aplicações:**
    - **Web:** Transfere dados entre servidores e aplicações web. 
    - **Bancos de dados:** Usado para armazenar e trocar dados em bancos de dados orientados a documentos, como o MongoDB, e em alguns bancos de dados relacionais. 
    - **Configuração:** Também pode ser usado para arquivos de configuração, como no VS Code. 

- **Comparado com XML:**
    Embora o XML também seja usado para troca de dados, o JSON é geralmente considerado mais leve e fácil de usar, especialmente em aplicações web.

- **Estrutura:**
    O JSON usa chaves e valores para representar dados, e pode conter objetos e arrays para estruturar informações mais complexas.