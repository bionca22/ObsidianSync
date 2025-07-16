**Dado – Definição**

É a menor unidade de armazenamento dentro de um banco de dados. É um aspecto que quando “olhado” sozinho, não tem significado, não tem sentido. Para que haja compreensão do dado, é sempre necessário fazer o processamento, a realização de algum tipo de operação com o dado.

![[Pasted image 20250225175112.png]]

**Informação – Definição**

A informação é o resultado de algum tipo de operação com o dado, ou seja, é sempre, através do processamento dos dados que se pode obter a informação.

![[Pasted image 20250225175324.png]]

**Conhecimento – Definição**

Ocorre quando utilizamos a informação para chegar a alguma conclusão, ou até mesmo, reconhecer algum tipo de comportamento e/ou padrão.

Através de análises estatísticas, como por exemplo, média, contagem, valor máximo, valor mínimo e taxas de porcentagem, das informações, chega-se ao conhecimento.

**Exemplo:**  Como o dia está quente e a probabilidade de chover é baixa, irei à praia.

---

**Sistemas Baseados Em Arquivos**

No dicionário, um arquivo é a “reunião dos dados de um computador que, com registro individual e organizados sob um formato específico, contém textos, tabelas, imagens, sons etc.”. Resumindo, podemos dizer, então, que arquivos são estruturas específicas de armazenamento de dados.

Os sistemas de arquivos existem desde os primórdios da computação, ou seja, desde 1950. Outro ponto importante é o meio onde estes arquivos ficam armazenados: Discos rígidos (HDs), CDs, disquetes, fitas magnéticas, _pendrives_, cartões perfurados etc., servem para armazenar estes dados e, qualquer falha nesses mecanismos pode causar a perda de todos os dados.

Outro ponto crucial que motivou a existência dos bancos de dados é que cada software possui um formato específico de arquivo, obrigando o usuário a ter aquele software para poder ler ou gravar em um determinado formato.

há muitas outras desvantagens em utilizar os sistemas de arquivos para armazenamento de dados, como:

- **Inconsistência e redundância de dados:** Aplicações evoluem com o tempo e há formatos demais, gerando, muitas vezes, repetição de dados
- **Dificuldade de acesso aos dados:** Os dados nos arquivos normalmente só podem ser acessados de uma forma e, às vezes, isso pode atrasar o acesso à informação
- **Isolamento dos dados:** Muitas vezes o compartilhamento de dados pode ser dificultado pois nem sempre quem os recebe possui o mesmo software (e/ou versão) para acessar.
- **Falta de integridade:** Realizar buscas de dados em arquivos pode resultar em dados duplicados ou ignorados, devido ao formato de como são gerados ou guardados.
- **Falta de atomicidade:** Nem sempre existem mecanismos de tratamento de erros (causados por qualquer motivo) em arquivos e os dados podem ser perdidos.
- **Falta de segurança:** Muitas vezes a proteção dos arquivos é responsabilidade do sistema operacional e, muitas vezes, dados sensíveis são rapidamente acessados.

E, por isso, usamos bancos de dados, cujas principais características serão apresentadas a seguir.

**Bancos de Dados**

Na década de 60 a IBM percebeu que os sistemas de arquivos tinham muitos problemas e começou a desenvolver pesquisas de como solucioná-los. Mas foi somente em 1970 que Edgar Todd, um importante pesquisador da IBM publicou um artigo intitulado “_A Relational Model of Data for Large Shared Data Banks”_ (Um modelo relacional de dados para grandes bancos de dados compartilhados). Neste artigo, Todd apresenta um modelo que se tornou, mais tarde, o princípio mais importante dos bancos de dados. Foi somente na década de 1980 que a IBM então lançou seus primeiros projetos comerciais de bancos de dados. Já no início do século XXI, com o “estouro” da internet, os bancos de dados e sistemas começaram a ganhar cada vez mais espaço no mercado (inclusive de entretenimento como o de jogos) e novos fabricantes começaram a surgir, com propostas das mais diversas.

A ideia dos bancos de dados é justamente suprir os problemas dos sistemas baseados em arquivos, garantindo itens como integridade dos dados, segurança no acesso aos dados, atomicidade, independência da linguagem de programação, concentração no armazenamento e desempenho. Mas lembre-se que os bancos de dados servem para armazenar dados e não conhecimento. O conhecimento, aqui, é extraído do conjunto de dados.

**Bancos de Dados – Principais Características**

Bom, um sistema de banco de dados (comumente chamado de database ou base de dados) é nada mais do que um grande software capaz de armazenar dados, de forma organizada. Estes dados podem ser acessados por qualquer programa que utiliza nosso banco e são armazenados numa estrutura específica, que chamamos de tabelas.

Tabelas são nada mais do que estruturas com linhas e colunas. As linhas armazenam os dados, enquanto as colunas servem para “categorizar” aquele dado. Um exemplo com dados arbitrários, neste caso, torna mais fácil o entendimento deste importante conceito:

![[Pasted image 20250226075253.png]]

Note, neste simples exemplo, que os dados dos carros estão armazenados em uma linha, mas cada coluna representa um tipo de dados diferente para este carro. Os dados ficam no cruzamento das linhas e colunas, ou seja, se você quiser saber o modelo do carro cuja placa é “ABC-1234”, basta cruzar esta linha com a coluna “Modelo” e, neste caso, obter o dado “A8”.

No mundo dos bancos de dados, chamamos as tabelas de entidade e as colunas de atributos.

**Conceito de Projeto**

Para este assunto, precisamos definir o que é “projeto” e nada melhor do que usar o guia mais completo e importante sobre o assunto, o famoso “PMBOK”, que em sua primeira página define projeto como “um esforço temporário empreendido para criar um produto, serviço ou resultado exclusivo” (PMBOK, 2017).

O PMBOK define, ainda, que todo projeto normalmente é dividido em fases e essas fases devem ser muito bem definidas, ou seja, cada fase de cada projeto deve ter um início, uma execução e uma finalização. Independentemente do modelo de gestão de projetos utilizado, normalmente os projetos são divididos em quatro grandes fases, conforme a figura:

![[Pasted image 20250226075520.png]]

**Projeto de Bancos de Dados**

Uma vez entendido o conceito de projeto de forma generalista, podemos incluir agora questões mais detalhadas sobre o projeto do banco de dados. Assim como qualquer projeto, os bancos de dados também precisam de um processo bem definido para implementação.

O projeto do banco de dados inicia-se, normalmente, já na fase de planejamento do projeto principal, ou seja, junto com o planejamento do produto ou serviço final. Normalmente dividimos as fases do projeto do banco de dados em quatro grandes etapas, conforme mostrado na figura:

![[Pasted image 20250226075723.png]]

**Análise de Requisitos**

Antes de mais nada é preciso levantar os requisitos que dão a ideia inicial do sistema. Mas o que é um requisito? É a lista de tudo que o sistema alvo deve ter ou fazer, ou seja, quais são as entidades, como elas se relacionam, quais as regras de negócio etc.

Nessa fase usamos diversas técnicas importantes, como por exemplo, entrevistas e muitas reuniões para entendermos os processos que realmente serão controlados por esse sistema, mesmo que um jogo! Não podemos esquecer que o sucesso das próximas etapas certamente dependerá do entendimento claro dessas necessidades e do levantamento dos requisitos. As técnicas de extração e categorização de requisitos serão abordadas numa aula específica para este fim.

Então para especificar um requisito funcional, é necessário identificar quais funções/ações que o software deve desempenhar. É importante ressaltar que as principais operações de manipulação de dados são conhecidas como CRUD(Create/Read/Update/Delete) e, na especificação de requisitos, tais operações são representadas pelas palavras Manter ou Gerenciar.

Ao especificar um requisito funcional é necessário colocar código, nome e descrição. Cada requisito funcional representa uma função diferente do sistema.

Para especificar requisitos funcionais, é necessário que:

- Identifique o código do requisito funcional com o prefixo RF e depois o número do requisito.
- Identifique o nome do requisito funcional.
- Faça a descrição do requisito, identificando quais operações devem ser realizadas pelo sistema e, se for o caso, também identifique quais dados devem ser armazenados.


![[Pasted image 20250301170432.png]]
#### Modelagem física

![[Pasted image 20250306074504.png]]

##### Cardinalidade

A cardinalidade mínima pode ser 0 (zero) ou 1 (um), enquanto a cardinalidade máxima pode ser 1 (um) ou N (“ene”), portanto as possibilidades são:

- **(0, 1)** 🡪 Indica que a entidade pode ter nenhum ou apenas um de outra
- **(0, n)** 🡪Indica que a entidade pode ter nenhum ou vários (mais de 1) de outra
- **(1, 1)** 🡪 Indica que a entidade precisa ter ao menos um e não mais que isso
- **(1, n)** 🡪 Indica que a entidade precisa ter ao menos um e no máximo vários.

![[Pasted image 20250306075911.png]]

![[Pasted image 20250306075947.png]]

Outro pequeno exemplo. Carro X Proprietário (chamado de pessoa aqui), mostrado na figura 9. Os atributos aqui foram suprimidos apenas para mostrar o grau de relação entre essas entidades. Note que o carro pode ter no mínimo um proprietário e no máximo um proprietário, também. Por outro lado, a pessoa (proprietário), neste exemplo, pode não ter nenhum carro ou ter vários carros, nesse caso representado por “N”

![[Pasted image 20250306080052.png]]


**Técnica de Ida e Volta para estabelecer a cardinalidade dos relacionamentos**

Identificar a cardinalidade do relacionamento entre as tabelas é fundamental para determinar a localização da chave estrangeira, lembrando que a chave estrangeira sempre fica do lado do “n”. Para essa tarefa vamos utilizar a técnica de Ida e Volta na leitura do relacionamento. Vamos analisar o exemplo das tabelas Empregado e Departamento.

Por força do negócio, podemos verificar que a tabela Empregado está relacionada com a tabela Departamento, ou seja, um empregado trabalha no departamento e o departamento possui empregados. Mas o problema é a identificação correta da cardinalidade entre essas tabelas. Abaixo, temos os exemplos das tabelas empregado e departamento.

Vamos ler o relacionamento no sentido da Ida, ou seja, do empregado para o departamento.

**IDA ----------------->**  
  
1 Empregado no mínimo trabalha em 1 Departamento e no máximo em 1 Departamento

![[Pasted image 20250306080428.png]]

Agora, vamos ler o relacionamento no sentido da Volta, ou seja, do departamento para o empregado.

**<-----------------------VOLTA**

1 Departamento no mínimo tem 0 Empregados e no máximo N Empregados

![[Pasted image 20250306080501.png]]

Perceba que o “n” ficou do lado da entidade empregado, portanto é nessa tabela que a chave estrangeira deverá ficar, conforme exemplo abaixo.

![[Pasted image 20250306080538.png]]

Note, no exemplo acima,  que a função da chave estrangeira é fazer o relacionamento entre as tabelas, daí a importância de estabelecer corretamente a cardinalidade do relacionamento.

#### Prática de Projeto de Banco de Dados com MER

Existem 3 níveis de modelagem: conceitual, lógico e físico. Cada um desses níveis mostra uma parte de como o projeto de banco de dados deve ser desenvolvido.

A modelagem conceitual é uma importante fase do projeto de banco de dados e modelar corretamente pode influenciar diretamente na qualidade. É preciso entender bem o conceito além de aprender como modelar corretamente um contexto.

O modelo conceitual foi proposto por Peter Chen em 1976, mas sofreu muitas atualizações ao longo do tempo. Lembre-se, também, que essa fase de modelagem é totalmente independente da tecnologia, ou seja, não importa qual banco de dados será utilizado no projeto, mas sim as entidades, atributos e relacionamentos em questão.

No “mundo real”, ou seja, onde nosso projeto está sendo empregado, os objetos possuem, essencialmente, três coisas: nome; características; e comportamentos. O nome é, de fato, o nome do objeto modelado (por exemplo: Livro, Aluno, Médico, Produto, Personagem etc.).

Já os atributos são as características relevantes que nossas entidades podem ter. Por exemplo, num sistema de bibliotecas, o livro pode possuir atributos como “título”, “resumo”, “ISBN”, “autor(es)”, “localização na biblioteca”, etc. Já o mesmo livro, numa loja tem, além destes atributos, o “preço”. Por isso o contexto é muito importante, pois os atributos são apenas os que fazem sentido para tal.

Os comportamentos dos objetos (os métodos) não são tão importantes para o mundo do banco de dados, embora eles possam influenciar diretamente como cada objeto se relaciona com os demais. Por exemplo, se um livro pode ser emprestado num sistema de biblioteca, então sabemos que existe um relacionamento direto de livro com alguma entidade que o recebe, como por exemplo, “aluno” e este relacionamento possui uma série de características, como prazo de empréstimo, multa por atraso etc.

#### A Modelagem
Apenas um retângulo com o nome da entidade ao centro basta para essa tarefa.

Agora os atributos devem ser modelados conforme exibidos na figura 2. Note que há dois tipos de atributos, um identificador e um comum. O atributo identificador é aquele cujos dados devem ser únicos (nunca se repetem) e nunca podem ser nulos (sem dados). Por exemplo: a placa de um carro, o CPF de uma pessoa, o ISBN de um livro etc. Já os atributos do tipo “comum” são aqueles que representam dados convencionais dessa entidade. Por exemplo, o nome de uma pessoa (pode se repetir), o modelo de um carro etc.

Uma vez compreendida as simbologias principais, agora é preciso juntar. A figura 3 representa como os atributos ficam em relação à entidade. Repare que o exemplo genérico mostra que há apenas um único atributo identificador, o que ocorre comumente.

![[Pasted image 20250308071431.png]]

Ainda falta mais um símbolo importante, o de relacionamento, neste caso representado na figura 4. Este símbolo ocorre entre duas entidades e denota que entre elas existe um grau de existência de uma em relação à outra. Por exemplo, um livro possui suas próprias características, assim como autor e podemos, portanto, ver estes como entidades distintas. De qualquer maneira, temos que relacionar um livro e um autor e, para isso, utilizamos este símbolo.

![[Pasted image 20250308071734.png]]

----

# reforço 
##### Cardinalidade

O termo cardinalidade vem da matemática que representa o número de elementos em um determinado conjunto. Por exemplo, o conjunto X = {2, 4, 6, 8, 20}, então dizemos que a cardinalidade é 5, pois este é o número de elementos dentro deste conjunto.

Na modelagem conceitual o conceito é o mesmo. Quantos elementos de uma entidade referem-se à outra entidade. Toda entidade que se relaciona com outra deve ter uma cardinalidade e, aqui, é representada em mínimo e máximo.

Usando o mesmo exemplo para explicar, de livro, temos a relação de ambos os lados, ou seja, do lado do livro e do lado do autor, conforme:

- O livro, para existir, precisa ter ao menos 1 autor e no máximo vários (indiferente) autores, ou seja, “N”.
- O autor, para ser considerado autor de livro, deve ter pelo menos 1 livro e no máximo vários livros, ou seja, “N”.

Isso quer dizer que estamos falando de uma relação “1 para N”, onde “N”, pode ser qualquer número inteiro natural. Lembre-se que na cardinalidade máxima não expressamos um número diferente de 1 ou N.

Para melhorar o entendimento, vamos a outro exemplo: Relação médico X paciente.

- O médico pode ter vários pacientes;
- Cada paciente pode ter vários médicos.

A cardinalidade na modelagem conceitual deve ser representada conforme a figura 7, ou seja, um parêntese, a cardinalidade mínima, uma “vírgula”, a cardinalidade máxima e o parêntese de fechamento.

![[Pasted image 20250308072027.png]]

A cardinalidade mínima pode ser 0 (zero) ou 1 (um), enquanto a cardinalidade máxima pode ser 1 (um) ou N (“ene”), portanto as possibilidades são:

- **(0, 1)** 🡪 Indica que a entidade pode ter nenhum ou apenas um de outra
- **(0, n)** 🡪Indica que a entidade pode ter nenhum ou vários (mais de 1) de outra
- **(1, 1)** 🡪 Indica que a entidade precisa ter ao menos um e não mais que isso
- **(1, n)** 🡪 Indica que a entidade precisa ter ao menos um e no máximo vários

Para ilustrar melhor o conceito e como incluir este grau de relação entre as entidades na modelagem conceitual, vamos continuar explorando o exemplo do livro X autor, conforme demonstrado na figura 8. Note que a cardinalidade ocorre de ambos os lados.

![[Pasted image 20250308072306.png]]

A cardinalidade que está próxima ao livro refere-se a do livro em relação ao autor e que está ao lado do autor refere-se à do autor em relação ao livro. Uma forma bastante usual de descobrir as cardinalidades é fazendo uma pergunta para a entidade e imaginando o que ela responderia: “Quantos você pode ter ao menos e no máximo da sua vizinha?”, por exemplo:

- Livro, você precisa ter quantos autores, pelo menos? 🡪  Um!
- Livro, você pode ter até quantos autores? 🡪 Vários

Do outro lado agora...

- Autor, você precisa ter ao menos quantos livros? 🡪 Um!
- Autor, quantos livros você pode ter? 🡪 Vários

Outro pequeno exemplo. Carro X Proprietário (chamado de pessoa aqui), mostrado na figura 9. Os atributos aqui foram suprimidos apenas para mostrar o grau de relação entre essas entidades. Note que o carro pode ter no mínimo um proprietário e no máximo um proprietário, também. Por outro lado, a pessoa (proprietário), neste exemplo, pode não ter nenhum carro ou ter vários carros, nesse caso representado por “N”

![[Pasted image 20250308072622.png]]


#### Técnica de Ida e Volta para estabelecer a cardinalidade dos relacionamentos

Identificar a cardinalidade do relacionamento entre as tabelas é fundamental para determinar a localização da chave estrangeira, lembrando que a chave estrangeira sempre fica do lado do “n”. Para essa tarefa vamos utilizar a técnica de Ida e Volta na leitura do relacionamento. Vamos analisar o exemplo das tabelas Empregado e Departamento.

Por força do negócio, podemos verificar que a tabela Empregado está relacionada com a tabela Departamento, ou seja, um empregado trabalha no departamento e o departamento possui empregados. Mas o problema é a identificação correta da cardinalidade entre essas tabelas. Abaixo, temos os exemplos das tabelas empregado e departamento.

![[Pasted image 20250308072814.png]]

Note, no exemplo acima,  que a função da chave estrangeira é fazer o relacionamento entre as tabelas, daí a importância de estabelecer corretamente a cardinalidade do relacionamento.

Vamos, agora, analisar outro exemplo. A área de negócio é uma escola, abaixo temos a especificação dos requisitos funcionais.

RF01- MANTER DADOS DO PROFESSOR

O sistema deve permitir a inclusão, alteração, exclusão e consulta dos dados dos professores. Sendo que estas operações serão realizadas pela secretária.

RF02- MANTER DADOS DO ALUNO

O sistema deve permitir a inclusão, alteração, exclusão e consulta dos dados dos alunos. Sendo que estas operações serão realizadas pela secretária.

RF03- MANTER DADOS DO CURSO

O sistema deve permitir a inclusão, alteração, exclusão e consulta dos dados dos cursos. Sendo que estas operações serão realizadas pela secretária.

RF04- MANTER DADOS DA MATRÍCULA

O sistema deve permitir a inclusão, alteração e consulta dos dados das matrículas.

RF05- MANTER DADOS DA DISCIPLINA

O sistema deve permitir a inclusão, alteração, exclusão e consulta dos dados das disciplinas. Sendo que estas operações serão realizadas pela secretária.

O primeiro passo é identificar as entidades, como já sabemos, uma entidade é uma representação de um conjunto de dados sobre determinado conceito do sistema. Algo que seja relevante para o negócio e que tenha mais de uma ocorrência. Toda entidade possui atributos, que são os dados que referenciam a entidade. Exemplos de Entidades: CLIENTE, PROFESSOR, ALUNO, CONSULTA, PACIENTE, PEDIDO, etc.

No exemplo da escola, devemos analisar o requisito funcional e identificar as entidades, realizando as seguintes perguntas:

- Para a escola é relevante armazenar os dados dos alunos? Existe mais de um aluno para ser armazenado?

- Para a escola é relevante armazenar os dados dos cursos? Existe mais de um curso para ser armazenado?

- Para a escola é relevante armazenar os dados dos professores? Existe mais de um professor para ser armazenado?

- Para a escola é relevante armazenar os dados das matrículas? Existe mais de uma matrícula para ser armazenada?

- Para a escola é relevante armazenar os dados das disciplinas? Existe mais de uma disciplina para ser armazenada?

Se as respostas dessas perguntas forem “sim”, significa que se trata de uma entidade. Portanto, chega-se à conclusão que ALUNO, PROFESSOR, CURSO, DISCIPLINA  e MATRÍCULA são entidades da Escola.

Depois de identificar as entidades, agora é necessário encontrar os atributos de cada entidade, lembrando que os atributos são características que descrevem, identificam, qualificam e/ou quantificam a entidade. São os dados que precisam ser armazenados sobre a entidade”. Exemplos de atributos: código, nome, endereço, sexo, data de nascimento, cpf, RA, valor unitário, etc.

No exemplo do cenário exemplo escola, devemos analisar o requisito funcional e identificar os atributos, realizando a seguinte pergunta:

- Quais dados devem ser armazenados para essa entidade? A resposta dessa pergunta foram os atributos da entidade.

No mínimo, cada entidade deve ter 2 atributos. Então podemos ter os seguintes dados:

Na entidade Aluno, encontramos os atributos: RA (Registro de Aluno), nome do aluno, data de nascimento e gênero.

Na entidade Professor, encontramos os atributos: RP (Registro de Professor), nome do professor, data de nascimento, gênero e  titulação.

Na entidade Curso, encontramos os atributos: código do curso, nome do curso, carga horário do curso.

Na entidade Disciplina, encontramos os atributos: código da disciplina, nome da disciplina, carga horária da disciplina.

Na entidade Matrícula, encontramos os atributos: código da matrícula, data da matrícula.

Depois de identificar as entidades e os atributos, chegamos ao momento de realizar o modelo conceitual, ou seja, representar as entidades e os seus relacionamentos.

![[Pasted image 20250308073541.png]]

![[Pasted image 20250308073618.png]]

Note, que o relacionamento entre as entidades DISCIPLINA e PROFESSOR é do tipo N:M, isso significa, que será necessário fazer um ajuste no modelo conceitual com a criação da entidade associativa, conforme se vê abaixo.

![[Pasted image 20250308073725.png]]

#### Modelagem Lógica

Antes de começar essa modelagem, é muito importante entender algumas coisas que serão utilizadas. Primeiro é preciso relembrar o conceito de entidade e atributo. As entidades representam os objetos do mundo real, enquanto seus atributos representam as características destes objetos. Por exemplo, num sistema de e-commerce, você pode ter a entidade chamada “Produto”, enquanto seus atributos possíveis podem ser “nome”, “fabricante”, “modelo”, “descrição”, “preço”, entre outros.

Não podemos esquecer também que existem essencialmente dois tipos de atributos: comum (ou tipo “dado”) e identificador (ou tipo “chave”).

O atributo do tipo comum é aquele que não possui nenhuma restrição importante na modelagem conceitual e representa um dado normalmente, daquela entidade. Já o atributo do tipo chave é aquele que identifica o conjunto de dados. Em uma tabela um atributo tipo chave não pode ser nulo e nem mesmo se repetir nunca. Por exemplo, no mesmo cenário de um e-commerce, como cada produto possui características que podem se repetir, podemos criar um novo atributo chamado “id_produto” para considerá-lo como chave. Neste caso, este “id” é único de um produto (regra de nunca se repetir) e nunca podem existir produtos sem este dado (regra de nunca ser nulo).

![[Pasted image 20250308074029.png]]

Para ilustrar como ficaria a tabela deste exemplo, alguns dados arbitrários e fictícios podem ser vistos na tabela 1. Note que a tabela se chama “Produto” e cada um dos atributos descritos no modelo conceitual se tornaram as colunas. Note, também, que nessa tabela de exemplo os nomes das colunas estão todos em letras minúsculas e sem quaisquer acentuação ou caracteres especiais. Embora seja apenas um exemplo, já está sendo exibido no padrão lógico. Note, também, que a coluna “id” possui uma cor diferente para representá-la como chave.

![[Pasted image 20250308074143.png]]

Lembre-se que a tabela anterior contém apenas exemplos arbitrários e está sendo usada apenas para referência. Note uma coisa importante nessa tabela: Cada coluna possui um tipo de dados específico. Isso é algo que devemos prestar bastante atenção na hora da modelagem lógica, pois os tipos de dados dependem da tecnologia de banco de dados que será utilizada. É por isso que durante a modelagem lógica já é preciso saber qual tecnologia de banco de dados será utilizada.

****Chave Estrangeira (FK)**

Na modelagem lógica um novo tipo de coluna aparece. As tão esperadas chaves estrangeiras ou, em sua nomenclatura original, _foreign keys_, as famosas FKs. É muito comum tratarmos esse tipo de coluna com o nome original em inglês ou, simplesmente, pela sigla dela.

As chaves estrangeiras são importantes pois são elas que representarão os relacionamentos entre as entidades (que agora começamos a chamar de tabelas). Sempre que estamos derivando o modelo conceitual para o lógico, teremos uma série de chaves estrangeiras em nosso modelo.

**Conceito importante sobre chave estrangeira:** Todas as colunas marcadas como “FK”, sempre apontam para uma coluna de chave primária (_primary key_ – PK), ou seja, os dados que são inseridos dentro das colunas do tipo “FK” são dados que apontam para outros dados, sempre identificadores (chave) de alguma outra entidade (relacionada) com a tabela que está recebendo essa FK. Eventualmente apontam para a mesma tabela, em auto relacionamentos.

Para melhor entendimento, vamos ao exemplo original do “produto”, mas agora será acrescido uma nova tabela chamada “categoria”.

![[Pasted image 20250310143417.png]]

Neste exemplo, fora adicionado uma entidade chamada categoria, onde o produto deve possuir no mínimo uma categoria e no máximo uma categoria, também. Por outro lado, a categoria pode não conter nenhum produto, mas também pode conter vários produtos. Para o relacionamento em questão, uma FK deve ser gerada na tabela de produto, ou seja, uma nova coluna deve ser incluída na tabela de produto indicando a qual categoria ele pertence, mas através de seu “id_categoria”. Para ilustrar essa ideia, veja a tabela categoria implementada com dados arbitrários.

Note que cada categoria, neste caso, possui um “id” que é único da categoria e, para satisfazer esse tipo de relacionamento, o “id_categoria” deve ser adicionado na tabela de produtos, conforme exemplificado com dados arbitrários da tabela 4. Isso quer dizer que a “id_categoria” na tabela de produtos é um FK para tabela “Categoria”. Neste modelo foi adicionada a FK na tabela “protudo” pois cada produto possui uma categoria, ou seja, o entendimento do contexto também é necessário para a inclusão dessa FK no local correto e indicada pela modelagem lógica, vista a seguir.

**Tipos de Relacionamentos que podemos encontrar no MER Lógico**

**Exemplo de Relacionamento 1:1**

No relacionamento 1:1, geralmente a chave estrangeira (FK) fica na entidade que contém (entidade forte), ou seja, do lado da entidade que existe sem depender da outra entidade relacionada. No exemplo abaixo, a disciplina existe independente do plano de ensino. Já, no caso, do plano de ensino, não faz sentido ter um plano de ensino sem a disciplina, por isso nesse exemplo a FK fica do lado da entidade forte, ou seja, na disciplina.

![[Pasted image 20250310163927.png]]

É importante ressaltar que em alguns casos de relacionamento 1:1, não se faz a separação em entidades diferentes, mas isso depende muito das regras específicas de funcionamento de cada negócio.

### 📌 Relacionamento 1:1 em Modelagem de Banco de Dados

> Em alguns casos de relacionamento **1:1**, não se faz a separação em entidades diferentes, mas isso depende das regras específicas do negócio.

####  O que é um Relacionamento 1:1?  
Um relacionamento **1:1** ocorre quando, para cada registro em uma tabela, há no máximo **um único registro correspondente** em outra tabela.

**Exemplo:**  
- Uma pessoa pode ter **um único CPF**, e um CPF pertence a **uma única pessoa**.

Na modelagem de banco de dados, podemos representar esse relacionamento de duas formas:  

1. **Separar em duas tabelas diferentes**  
   - Criamos tabelas distintas com uma **chave primária compartilhada**.  
   - Exemplo: Tabela `Pessoa` e tabela `Documento` com `CPF` como chave estrangeira.  

2. **Manter tudo em uma única tabela**  
   - Apenas adicionamos os atributos da segunda entidade na tabela principal.  
   - Exemplo: A tabela `Pessoa` já contém a coluna `CPF`, sem precisar de outra tabela.

#### Quando **Não** Separar em Entidades Diferentes?  
A decisão de manter os dados juntos em uma única tabela ou separá-los **depende das regras do negócio**.  

> [!tip] Quando **não** separar?  
> - **Os dados sempre existirão juntos** (não há registros sem correspondência).  
> - **A separação não melhora o desempenho ou a organização**.  
> - **Evita consultas desnecessariamente complexas** ao unir as tabelas.  

#### Exemplo Prático  
Imagine um sistema de cadastro de funcionários onde **cada funcionário tem um crachá único**. Como **todo funcionário terá obrigatoriamente um crachá e vice-versa**, **não há necessidade de criar duas tabelas separadas** (`Funcionario` e `Cracha`).  

> [!example] Melhor solução  
> Adicionar o campo `numero_cracha` diretamente na tabela `Funcionario`.  

Porém se o crachá **pudesse ser reutilizado por diferentes funcionários** (exemplo: crachás temporários para visitantes), então **separar as tabelas seria mais justificado**.

> [!warning] Cuidado!  
> Se os dados podem mudar de relacionamento ao longo do tempo, manter tabelas separadas pode evitar problemas futuros.

**Relacionamento 1:N ou N:1**

No relacionamento 1:N, a chave estrangeira sempre fica do lado do N.

![[Pasted image 20250310165557.png]]

**Exemplo de Relacionamento N:M**

N:N = muitos para muitos

No relacionamento N:M, é necessário criar uma entidade associativa, que via de regra, é formada pela composição das chaves primárias das entidades envolvidas no relacionamento, que vem como chaves estrangeiras formando uma chave primária composta, além dos atributos próprios dessa entidade.

![[Pasted image 20250310170300.png]]

**Modelagem Física**

O modelo físico contém todos os scripts de comandos, que permitem a implementação física do banco de dados. Esse nível de modelagem é completamente dependente do SGBD.

Vamos ver um exemplo prático da derivação de Modelo lógico e físico. Analise o modelo entidade relacionamento lógico da fábrica de autopeças, gere e implemente o modelo físico, além de fazer a população das tabelas criadas.

![[Pasted image 20250310170352.png]]

Ao fazer o modelo físico, é necessário conhecer as regras de nomenclatura do SGBD e, se for o caso, ajustar os nomes dos atributos do modelo lógico para o modelo físico. As regras de nomenclatura, mudam de um SGBD para outro, mas as principais regras são:

- nome de objeto não pode começar com número;

- não pode haver objetos com nomes duplicados;

- não pode usar palavras reservadas para nomear objetos;

- somente os caracteres especiais _,$ e # podem ser utilizados nos nomes;

- nomes dos objetos podem ter letras e números;

- quanto ao tamanho, depende muito do SGBD, mas por exemplo no Oracle, a partir da versão 10g, é possível criar objetos com 128 caracteres.

Ao fazer o modelo físico, primeiro crie as entidades fortes, depois as entidades fracas e por fim as entidades associativas. Então, no exemplo, da fábrica de autopeças, a ordem de criação deve ser : Cliente,Vendedor,Deposito,Pedido,Peca e Pedido_Peca.

Uma técnica utilizada, para não se preocupar com a ordem de criação das tabelas, é criar as tabelas sem nenhuma constraint e depois de criar todas as tabelas executar o comando alter table e adicionar as constraints de pk´s e fk´s.

Abaixo, temos um exemplo de modelo lógico, dentro do BRmodelo, do estudo de caso da fábrica de autopeças.

![[Pasted image 20250310171938.png]]

**Exemplo de Geração de Modelo físico**

Observe que primeiro são criadas as entidades fortes, depois as entidades fracas e por fim as entidades associativas. É muito importante, respeitar essa ordem na criação das tabelas, para não ter erros de violação de constraints (restrições de integridade).

```
CREATE TABLE VENDEDOR (

Cod_do_Vendedor number(5) PRIMARY KEY,

Nome_do_Vendedor varchar2(50),

Endereco varchar2(50),

Percentual_de_Comissao number(2,1)

);

CREATE TABLE CLIENTE (

Cod_do_Cliente number(5) PRIMARY KEY,

Nome_do_Cliente varchar2(50),

Endereco_do_Cliente varchar2(50),

Limite_de_Credito number(9,2),

Faturamento_Acumulado number(9,2)

);

CREATE TABLE DEPOSITO (

Cod_do_Deposito number(5) PRIMARY KEY,

Endereco_do_deposito varchar2(50)

);

CREATE TABLE PECA (

Cod_da_Peca number(5) PRIMARY KEY,

Preco_Unitario_da_Peca number(9,2),

Descricao_da_Peca varchar2(50),

Quantidade_em_Estoque number(5),

Cod_do_Deposito number(5) REFERENCES DEPOSITO (Cod_do_Deposito)

);

CREATE TABLE PEDIDO(

Cod_do_Pedido number(5) PRIMARY KEY,

Cod_do_Cliente number(5) references Cliente (cod_do_cliente),

Cod_do_Vendedor number(5) references Vendedor (cod_do_vendedor),

Data_do_Pedido date

);

CREATE TABLE PEDIDO_PECA (

Cod_da_Peca number(5) references peca(cod_da_peca),

Cod_do_Pedido number(5) references pedido (cod_do_pedido),

Qtde_de_Pecas_solicitadas number(5),

Preco_cotado_da_Peca number(9,2),

PRIMARY KEY(Cod_da_Peca,Cod_do_Pedido)

);
```

Verifique que o esquema físico foi gerado com os comandos de criação de todas as tabelas que constavam no modelo lógico.
![[aulas.descomplica.com.br-Prática de Projeto de Banco de Dados com MER.pdf]]

[^1]: 
