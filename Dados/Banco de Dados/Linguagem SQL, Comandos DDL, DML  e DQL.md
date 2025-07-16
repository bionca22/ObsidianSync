
#### Linguagem SQL e Comandos DDL

É através da linguagem SQL que interagimos com o SGBD. Essa linguagem é composta de categorias de comandos. São elas DDL (comandos de definição de estruturas), DML (comandos de manipulação de dados, DCL (comandos de controle) e DQL (comandos de consulta).

Conhecer os comandos da linguagem SQL é fundamental para acessar o SGBD, manipular estruturas de armazenamento e seus dados.

**DDL – Data Definition Language – Trabalhando Com Tabelas**

A DDL é a parte da SQL usada para criar e manipular objetos que se relacionam aos dados, especialmente tabelas. Com a DDL você pode criar uma tabela, configurar suas colunas e todas as restrições de integridade, por isso antes de começarmos a escrever nossos primeiros comandos temos que entender bem a linguagem SQL e as restrições de integridade envolvidas.

A DDL está intimamente ligada também a modelagem física do banco de dados, pois é nessa parte do projeto onde os modelos lógicos são derivados para um banco de dados real, ou seja, se tornam físicos (saem do papel).

Vamos começar entendendo a sintaxe do comando que é capaz de criar uma tabela, o CREATE TABLE, que funciona da seguinte forma:

![[Pasted image 20250311090907.png]]

Para entender melhor este comando, vamos utilizá-lo em um modelo real. A modelagem conceitual pode ser vista na figura 1, onde estamos criando a base de dados de um pequeno jogo, onde cada personagem é de um tipo e possui um ou mais poderes (somente esta parte do jogo). A figura 2 mostra a derivação do respectivo contexto para a modelagem lógica.

![[Pasted image 20250311092519.png]]

Vamos começar a implementação física deste cenário pela tabela mais simples, ou seja, a que possui menos restrições e não depende de nenhuma outra tabela para existir. Neste caso temos as tabelas “tipo” e “poder”. A tabela “personagem”, por exemplo, possui uma chave estrangeira para “tipo” e, por isso, não poderíamos começar por ela, a não ser que façamos a inclusão da restrição referencial depois, alterando-a.

![[Pasted image 20250311092936.png]]

Repare que assim como na modelagem lógica, a restrição da chave primária recebe um nome, nesse caso “tipo_pk”. Isso ocorre nas restrições de chave e referencial. Ao se incluir a restrição de chave é necessário informar qual é a coluna que recebe essa restrição, neste caso a coluna “idTipo”. Seguindo a mesma lógica, criamos as próximas tabelas.

![[Pasted image 20250311093114.png]]

![[Pasted image 20250311093135.png]]

Repare na criação da tabela “personagem” que há a restrição referencial sendo aplicada com o acréscimo da CONSTRAINT do tipo FOREIGN KEY. Lembre-se que toda restrição, no Oracle, deve ter um nome e, no caso da chave estrangeira, é preciso informar qual coluna local a recebe e qual o “alvo”, ou seja, a tabela e sua respectiva coluna de chave primária.

Por fim, vamos criar a tabela de relacionamento entre “personagem” e “poder”, pois como a relação é N:N (cada personagem pode possuir N poderes e cada poder pode estar associado a N personagens), temos que as relacionar através de uma terceira tabela, conforme:

![[Pasted image 20250311093321.png]]

Repare nas quebras de linhas e a indentação (afastamento da margem) são diferentes para cada comando. Isso quer dizer que não importa se as linhas estão quebradas ou não para a execução do script, mas aqui são descritas assim para maior legibilidade. Essa é, inclusive, uma forte recomendação da comunidade internacional e de qualquer manual de bancos de dados. Repare, ainda, que todos os comandos foram escritos com letras maiúsculas e isso também poderia ter sido diferente, ou seja cada comando poderia ter sido escrito completamente em letras minúsculas, mas por boas práticas de programação escrevemos as palavras reservadas da SQL em letras maiúsculas e o nome dos objetos criados por nós mesmos em letras minúsculas. Por fim, e não menos importante, repare que ao final de cada comando há um “;” que especifica sua finalização.

Se você precisar excluir uma tabela, deve-se utilizar o comando “DROP TABLE nome_da_tabela;”, por exemplo “DROP TABLE tipo;” e a tabela tipo será eliminada do banco de dados. Deve-se utilizar este comando com muito cuidado.

Para se alterar dados de uma tabela, utiliza-se o comando “ALTER TABLE nome_da_tabela MODIFY (modificações);”. A palavra reservada “MODIFY” pode ser substituída por “ADD” se você está adicionando algo na tabela. Por exemplo, se você precisa alterar que a altura do personagem não pode ser nula, deve-se executar o comando “ALTER TABLE personagem MODIFY (altura NOT NULL);” e se você precisar acrescentar uma nova coluna chamada “idade” (que refere-se à idade da personagem), o comando “ALTER TABLE personagem ADD idade NUMBER(2) NULL;” deve ser executado.

Na criação de tabelas, usa-se um comando  DDL. Para criar uma tabela é necessário que o usuário tenha privilégio e uma área para armazenamento. A sintaxe simplificada para criação de tabelas é:


`**Sintaxe: CREATE TABLE** [_esquema._]_tabela_`
          `(nome da coluna _tipo do  dado_ [DEFAULT _expr_]`
              `_[constraint da coluna],_`
              `_...,_`
              `_[constraint da tabela]);_`

onde:

|   |   |
|---|---|
|_Esquema:_|é o  nome do proprietário da tabela, quando omitido a tabela é criada no esquema do usuário corrente|
|_Tabela:_|é o nome da tabela|
|_DEFAULT expr:_|especifica um valor default que será utilizado quando um dado for omitido na inserção|
|_Coluna:_|é o nome da coluna|
|_tipo de dados:_|é o tipo de dados e o comprimento da coluna|
|_Constraint:_|Está cláusula é opcional e especifica as restrições para a coluna ou para a tabela, quando o nome da constraint é omitido o Oracle assume uma identificação|

Convenções para Nomeação de Tabelas e Colunas:

• Deve começar com uma letra

• Pode ter de 1 a 30 caracteres (depende do SGBD)

• Deve conter somente A–Z, a–z, 0–9, _, $ e #

• Não deve duplicar o nome de outro objeto de propriedade do mesmo usuário

• Não deve ser uma palavra reservada pelo Oracle Server

Tipos de Dados:

![[Pasted image 20250311093856.png]]


No exemplo abaixo está sendo criada  a tabela DEPT, com três colunas — chamadas, DEPTNO, DNAME e LOC.

SQL>CREATE TABLE dept  
  2      (deptno NUMBER(2),

  3      dname          VARCHAR2(14),

  4      loc      VARCHAR2(13));

Table created.

A instrução Describe é utilizada para exibir a estrutura de uma tabela.

SQL> DESCRIBE dept

Name                Null?    Type

------------------ -------- ---------

DEPTNO                      NUMBER(2)

DNAME                       VARCHAR2(14)

LOC                         VARCHAR2(13)

---
**Restrições de Integridade**

São elas chaves primárias, chaves estrangeiras, colunas de dados únicos, não nulos etc., especialmente na modelagem lógica. Quando uma restrição é “violada” (não é atendida) é muito mais fácil encontrarmos a origem do erro. Os bancos de dados chamam as restrições com seu termo em inglês, ou seja, “CONSTRAINT”.

As restrições de integridade servem para impedir que dados inválidos sejam inseridos numa determinada coluna e são garantidas pelo próprio SGBD (Sistema Gerenciador de Banco de Dados), nós apenas as configuramos na hora de criar os objetos (através da DDL). Podemos, inclusive, dizer que as restrições (CONSTRAINTS) impõem regras nas colunas. Essas restrições são divididas em seis grupos, sendo:

- Restrição de integridade de **domínio**
- Restrição de integridade de **chave**
- Restrição de integridade **nula**
- Restrição de integridade **referencial**
- Restrição de integridade **unicidade**
- Restrição de integridade **de valor padrão**

A integridade de domínio especifica qual **tipo de valor** um determinado atributo pode admitir, ou seja, é são os tipos de dados (datatypes). Por exemplo, colunas configuradas como número inteiro, número de ponto flutuante, texto, data com hora, somente data, etc. Se um dado do tipo texto for inserido em uma coluna que aceita apenas valores numéricos, a restrição de integridade de domínio será violada. A integridade de domínio pode ir além, podendo **checar** se um valor inserido está dentro de uma especificação. Para isso, utiliza-se a restrição “CHECK”. Por exemplo, o estado no cadastro de um endereço, deve ser uma das 27 opções; o sexo de uma pessoa etc.

A integridade de vazio especifica se o valor de um atributo **pode ou não ser vazio**, ou seja, nulo. São os famosos NULL (permite que um dado seja vazio) e NOT NULL (não permite que um dado não seja especificado naquela coluna na hora de inserir uma linha). A integridade de vazio é também associada à cardinalidade mínima nos relacionamentos (0, a FK pode ser nula. 1, a FK não pode ser nula).

Já a integridade de chave (ou como alguns autores chamam, integridade de chave primária) garante que os valores das chaves primárias sejam sempre únicos e não nulos, pela própria definição de chave primária. Por exemplo, se tentarmos inserir uma linha cuja chave primária já exista, haverá violação da restrição de chave primária.

A integridade referencial é a integridade das FKs (chaves estrangeiras – _Foreign Keys_). Ela garante que o valor que aparecer nos atributos de uma chave estrangeira deve sempre aparecer na chave primária da tabela referenciada, ou seja, garante que todo valor de uma FK seja o mesmo de uma PK, a qual a coluna em questão aponta. Assim sendo, sempre que uma coluna é definida como FK, o SGBD deve garantir que ela sempre aponte para uma PK. Na hora que estamos criando as colunas FKs devemos dizer qual é a tabela alvo e sua respectiva chave primária.

A integridade de unicidade é aquela restrição que permite, ou não, que o valor se repita. No banco de dados utilizamos a palavra reservada UNIQUE quando queremos que seus dados sejam únicos, como por exemplo, o RG de uma pessoa, o e-mail de um usuário, os dados de uma impressão digital etc. Não confunda a restrição de unicidade com a de chave primária, pois os valores dessa coluna não são necessariamente identificadores da tabela.

Por fim e não menos importante temos a integridade de valor padrão associada à palavra reservada DEFAULT. Essa restrição permite que se um valor nulo for inserido em uma coluna (ou não foi informado, por exemplo) um valor padrão (pré-definido) é colocado em seu lugar. Por exemplo, se o país não foi informado numa tabela de endereços incluir “Brasil”. Essa restrição está fortemente ligada à restrição de nulo.

É muito importante reforçar que todas as restrições de integridade são garantidas pelo próprio SGBD. Uma restrição que não se encaixa em nenhuma das citadas aqui é chamada de restrição semântica e deve ser garantida pelo software que utiliza o banco de dados. Por exemplo, a cardinalidade máxima de um relacionamento ou, ainda como exemplo real, imagine que temos um relacionamento entre funcionários e departamento, onde um funcionário de recursos humanos não poderia assumir o cargo de analista de sistemas. Essa é uma restrição que deve ser garantida pela própria aplicação.

Pockt Guide

![[Pasted image 20250311095133.png]]

![[Pasted image 20250311095202.png]]

----

# Comandos DML  e DQL

**Introdução** 

É através da linguagem SQL que interagimos com o SGBD. Essa linguagem é composta de categorias de comandos. São elas DDL (comandos de definição de estruturas), DML (comandos de manipulação de dados, DCL (comandos de controle) e DQL (comandos de consulta).

Conhecer os comandos da linguagem SQL é fundamental para acessar o SGBD, manipular estruturas de armazenamento e seus dados.

**Comandos DML**

Os comandos da categoria DML (Data Manipulation Language), servem para realizar  adições, eliminações e atualizações em dados de um ou mais registros de uma ou mais tabelas de maneira concorrente. Os comandos da categoria DML são:

- Insert – Adição de linhas com  dados na tabela
- Update – Atualização de  dados na tabela
- Delete – Eliminação de dados da tabela
- Commit – Confirmação das transações, ou seja, salvamento dos dados
- Rollback – Desistência das transações, ou seja, desfazer a última transação

**A adição de linhas com dados é um comando DML.**

**Sintaxe:**

**INSERT INTO** _tabela_ [(_coluna_ [_, coluna..._])] **VALUES** _(valor_ [_, valor..._])_;_

Onde:

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1693227350131-XB2TF5sprq.png)


### **Verificando a estrutura de uma tabela**

Para visualizar a ordem padrão das colunas e os tipos de dados esperados, utilize o comando `DESCRIBE`:

```
SQL> DESCRIBE dept;
```

📌 **Saída do comando:**

|Nome da Coluna|Permite Nulo?|Tipo de Dado|
|---|---|---|
|**DEPTNO**|NOT NULL|NUMBER(2)|
|**DNAME**|NULL|VARCHAR2(14)|
|**LOC**|NULL|VARCHAR2(13)|

🔹 O comando `DESCRIBE` exibe:

- A **ordem das colunas** na tabela.
- Se a coluna aceita valores **NULL**.
- O **tipo de dado** definido para cada campo.

💡 **Dica:** Sempre use `DESCRIBE` antes de inserir dados para garantir que os valores inseridos correspondam ao tipo esperado.


**Exemplo 1: Inserção completa com colunas especificadas**

```
SQL> INSERT INTO dept (DEPTNO, DNAME, LOC)  
  2  VALUES (80, 'COMERCIAL', 'SP');
```

🔹 Neste exemplo, estamos inserindo um novo departamento (**DEPTNO 80**) chamado **"COMERCIAL"**, localizado em **"SP"**.


**Exemplo 2: Inserção sem especificar colunas (assumindo a ordem da tabela)**

```
SQL> INSERT INTO dept  
  2  VALUES (90, 'FINANCEIRO', 'RJ');
```

🔹 Aqui, os valores estão sendo inseridos diretamente, assumindo que a tabela **`dept`** possui exatamente três colunas na ordem correta (**DEPTNO, DNAME e LOC**).

📌 **Recomendação:** Sempre que possível, especifique os nomes das colunas para evitar problemas caso a estrutura da tabela mude no futuro.

### **Inserção de Dados em Tabelas**


**Exemplo 3: Inserção parcial de dados**

```
SQL> INSERT INTO dept (deptno, dname)  
  2  VALUES (55, 'RH');
```

🔹 A tabela **`dept`** contém as colunas **`deptno`**, **`dname`** e **`loc`**.  
🔹 Como o campo **`loc`** não foi especificado, ele será preenchido automaticamente com **NULL**.


**Exemplo 4: Inserção com valor NULL explícito**

```
SQL> INSERT INTO dept  
  2  VALUES (45, 'DIRETORIA', NULL);
```

🔹 Aqui, os valores estão sendo inseridos diretamente, e o campo **`loc`** recebe **NULL** explicitamente.  
🔹 Isso é útil quando queremos deixar claro que o campo não terá um valor atribuído.


## **Inserção de Dados com Datas**

 **Exemplo 5: Inserindo um registro na tabela `emp`**

```
SQL> INSERT INTO emp  
  2  VALUES (3000, 'JOSE', 'VENDEDOR', 7782, TO_DATE('30/03/23', 'DD/MM/YY'),  
  3          2800, NULL, 20);
```

🔹 **Explicação dos valores inseridos:**

- `3000` → Código do empregado.
- `'JOSE'` → Nome do empregado.
- `'VENDEDOR'` → Cargo.
- `7782` → Código do gerente.
- `TO_DATE('30/03/23', 'DD/MM/YY')` → Data de admissão (convertida para formato de data).
- `2800` → Salário.
- `NULL` → Comissão (não aplicável).
- `20` → Código do departamento.

### **Visualizando os dados inseridos:**

Para verificar os registros na tabela **`emp`**, use:

```
SQL> SELECT *  
  2  FROM emp;
```

## **Atualização de Dados nos Registros**

**Sintaxe do comando `UPDATE`**

```
UPDATE tabela  
SET coluna = valor [, coluna = valor, ...]  
[WHERE condição];  
```

🔹 **Importante:** Se a cláusula `WHERE` for omitida, **todas as linhas** da tabela serão alteradas!

### **Exemplo: Atualizando um registro específico**

Atualizar o departamento para **30** do empregado com código **7900**:

```
SQL> UPDATE emp  
  2  SET deptno = 30  
  3  WHERE empno = 7900;
```

📌 **Sempre utilize a cláusula `WHERE` ao atualizar registros para evitar modificar toda a tabela por engano.**

### **Comando `SELECT`**

O comando `SELECT` é utilizado para realizar consultas aos dados armazenados em uma tabela.

**Exemplo de `SELECT` exibindo todos os dados da tabela `emp`**

```
SQL> SELECT *  
  2  FROM emp;
```

🔹 O asterisco (`*`) indica que **todas as colunas** da tabela serão retornadas na consulta.

## **Sintaxe do Comando `SELECT`**

🔹 **Regras para uso dos comandos SQL:**

- O SQL **não diferencia maiúsculas e minúsculas** no processamento dos comandos.
- Os comandos podem ser escritos em **uma ou mais linhas**.
- **Não é permitido abreviar** as palavras-chave dos comandos.
- **Escrever cada parte do comando em uma linha separada** melhora a legibilidade.
- Para exibir **apenas colunas específicas**, devemos nomeá-las na consulta.

 **Exemplo: Exibir apenas algumas colunas**
```
SQL> SELECT deptno, dname  
  2  FROM dept;
```

🔹 Aqui, estamos consultando apenas as colunas **`deptno`** (número do departamento) e **`dname`** (nome do departamento).

# **Operadores Aritméticos**

Os operadores aritméticos podem ser utilizados em qualquer cláusula de uma instrução SQL, **exceto na cláusula `FROM`**.

![[Pasted image 20250315082302.png]]

 **Exemplo: Exibir o salário original e o salário acrescido de R$ 300,00**

``` SQL
SQL> SELECT ename, sal, sal + 300  
  2  FROM emp;
```

![[Pasted image 20250315082338.png]]
➡️ **Nova coluna gerada apenas para exibição:** O resultado apresentará os nomes dos empregados (**`ename`**), seus salários originais (**`sal`**) e uma **coluna extra** mostrando os salários com um acréscimo de R$ 300,00.

### **Ordem de precedência matemática**

As regras matemáticas e a ordem de precedência continuam válidas dentro do SQL.

``` SQL
 SQL> SELECT ename, sal, sal + ((sal * 30) / 100)  
  2  FROM emp;
```

➡️ Aqui, estamos calculando o salário acrescido de **30%**.

✅ **Dica:** Use **parênteses** para garantir a ordem correta dos cálculos.

# **Operadores de Comparação**

Os operadores de comparação são utilizados para **estabelecer relações entre valores ou expressões**.

- O resultado de uma comparação é sempre um valor **booleano** (`TRUE` ou `FALSE`).
- Podem ser usados em **comparações que envolvem apenas uma linha**.

![[Pasted image 20250315082444.png]]

### **Operador `BETWEEN`**

Os valores especificados com `BETWEEN` são **inclusivos**. O limite **inferior** deve ser especificado primeiro.

```SQL
SQL> SELECT ename, sal  
  2  FROM emp  
  3  WHERE sal BETWEEN 1000 AND 1500;
```

➡️ Retorna os funcionários cujo salário está **entre R$ 1.000 e R$ 1.500** (inclusive).

### **Operador `IN`**

Verifica se um valor está presente em uma **lista de valores específicos**.

```SQL
SQL> SELECT empno, ename, mgr, deptno  
  2  FROM emp  
  3  WHERE ename IN ('FORD', 'ALLEN');
```

➡️ Retorna os funcionários cujo nome seja **"FORD"** ou **"ALLEN"**.

✅ Se forem utilizados **caracteres ou datas**, eles devem estar entre **aspas simples (`'`)**:

```SQL
SQL> SELECT empno, ename, mgr, deptno  
  2  FROM scott.emp  
  3  WHERE job IN ('PRESIDENT', 'MANAGER');
```

➡️ Retorna funcionários cujo cargo (`job`) seja **"PRESIDENT"** ou **"MANAGER"**.

### **Operador `LIKE`**

O operador `LIKE` permite buscar registros que **correspondam a um padrão de caracteres**.

```SQL 
SQL> SELECT ename  
  2  FROM scott.emp  
  3  WHERE ename LIKE 'J%';
```

➡️ Retorna todos os funcionários cujo nome começa com **"J"** (letra maiúscula).  
🔹 Se houver nomes iniciados com **"j" minúsculo**, eles **não serão retornados**.

✅ **Símbolos utilizados no `LIKE`**:

- `%` → Representa **qualquer sequência de caracteres**.
    - Exemplo: `'A%'` encontra **"Ana"**, **"Antonio"**, **"Alberto"**, etc.
- `_` → Representa **um único caractere**.
    - Exemplo: `'A_'` encontra **"Ao"**, **"An"**, mas não **"Ana"**.

---

### **Operador `IS NULL`**

Usado para verificar campos que **não possuem valor** (`NULL`).

```SQL
SQL> SELECT ename, job, deptno  
  2  FROM scott.emp  
  3  WHERE comm IS NULL;
```

➡️ Retorna os funcionários que **não recebem comissão** (`comm` está `NULL`).

✅ **Importante:** `NULL` significa **ausência de valor**.  
❌ **Não podemos usar `=` ou `!=` para comparar valores `NULL`**, pois `NULL` **não é igual nem diferente de nada**.

# **Operadores Lógicos**

Os operadores lógicos permitem combinar múltiplas condições para gerar um **único resultado**.  
✅ **Principais operadores lógicos no SQL:**

1. **`AND`** → Ambas as condições devem ser **verdadeiras**.
2. **`OR`** → Pelo menos **uma** das condições deve ser verdadeira.
3. **`NOT`** → Inverte o resultado da condição.

 **Exemplo: Filtrar funcionários com salário maior que 2000 e que pertencem ao departamento 30**

```SQL
SQL> SELECT ename, sal, deptno  
  2  FROM emp  
  3  WHERE sal > 2000 AND deptno = 30;
```

➡️ Apenas os funcionários do **departamento 30** com **salário superior a R$ 2.000** serão retornados.

# **Operadores Lógicos no SQL**

Os operadores lógicos são utilizados para **combinar expressões** na cláusula `WHERE`. Eles podem ser aplicados em **consultas (`SELECT`)**, **atualizações (`UPDATE`)** e **exclusões (`DELETE`)** de dados.

## **Operador `AND`**

O operador `AND` retorna resultados **apenas quando todas as condições são verdadeiras**.

**Exemplo: Selecionar funcionários com salário ≥ 1100 e cargo `SALESMAN`**

```SQL
SQL> SELECT empno, ename, job, sal  
  2  FROM scott.emp  
  3  WHERE sal >= 1100 AND job = 'SALESMAN';
```

✅ **Resultado:**

``` 
EMPNO     ENAME      JOB        SAL  
7876      ADAMS      SALESMAN   1100  
7934      MILLER     SALESMAN   1300  
```

- Apenas os funcionários que atendem **ambas as condições** (`sal >= 1100` **E** `job = 'SALESMAN'`) são selecionados.
- Se qualquer condição for **falsa**, a linha não será incluída no resultado.

⚠️ **Cuidado com maiúsculas e minúsculas em valores alfanuméricos!**

- SQL **distingue letras maiúsculas e minúsculas**. No exemplo acima, `SALESMAN` deve estar em **maiúsculas**, caso contrário, nenhum resultado será retornado.

## **Operador `OR`**

O operador `OR` retorna resultados **quando pelo menos uma das condições for verdadeira**.

**Exemplo: Selecionar funcionários com salário ≥ 1100 ou cargo `SALESMAN`**

``` SQL
 SELECT empno, ename, job, sal  
  2  FROM emp  
  3  WHERE sal >= 1100 OR job = 'SALESMAN';
```

✅ **Resultado (parcial):**

```
EMPNO     ENAME     JOB         SAL  
7839      KING      PRESIDENT   5000  
7698      BLAKE     MANAGER     2850  
7782      CLARK     MANAGER     2450  
7566      JONES     MANAGER     2975  
7654      MARTIN    SALESMAN    1250  
...
```

- Se um funcionário **tiver salário ≥ 1100** **OU** **for `SALESMAN`**, ele será incluído no resultado.
- Funcionários que atendem **apenas uma das condições** também aparecem na consulta.

## **Operador `NOT`**

O operador `NOT` **inverte o resultado de uma condição**.

### **Exemplo: Selecionar funcionários que NÃO sejam `CLERK`, `MANAGER` ou `ANALYST`**

```
SQL> SELECT ename, job  
  2  FROM scott.emp  
  3  WHERE job NOT IN ('CLERK', 'MANAGER', 'ANALYST');
```

✅ **Resultado:**

```
ENAME      JOB  
KING       PRESIDENT  
MARTIN     SALESMAN  
ALLEN      SALESMAN  
TURNER     SALESMAN  
WARD       SALESMAN  
```

- **Apenas os funcionários que NÃO possuem os cargos listados** (`CLERK`, `MANAGER`, `ANALYST`) aparecem no resultado.

✅ **`NOT` pode ser combinado com outros operadores:**

```
... WHERE job   NOT IN ('SALESMAN', 'MANAGER');  -- Exclui SALESMAN e MANAGER  
... WHERE sal   NOT BETWEEN 2500 AND 5000;      -- Exclui salários entre 2500 e 5000  
... WHERE ename NOT LIKE '%S%';                 -- Exclui nomes que contenham "S"  
... WHERE comm  IS   NOT NULL;                  -- Seleciona funcionários com comissão  
```

# **Controle de Transações (COMMIT & ROLLBACK)**

As transações garantem que um conjunto de operações **DML** (`INSERT`, `UPDATE`, `DELETE`) seja executado corretamente no banco de dados.

### **Requisitos das transações:**

✔ **Consistência** → Os dados devem permanecer íntegros.  
✔ **Atomicidade** → Todas as operações devem ser concluídas com sucesso ou nenhuma será realizada.  
✔ **Integridade** → O banco de dados deve sempre manter um estado válido.

🚀 **Exemplo prático: Transferência de dinheiro**

1. Debita um valor da conta A (`UPDATE` na conta de origem).
2. Credita o mesmo valor na conta B (`UPDATE` na conta de destino).
3. **Se ambos os passos forem bem-sucedidos**, a transação é **confirmada (`COMMIT`)**.
4. **Se houver erro**, a transação é **desfeita (`ROLLBACK`)**.

---

## **COMMIT & ROLLBACK**

📌 **COMMIT** → Confirma as alterações no banco de dados de forma permanente.  
📌 **ROLLBACK** → Desfaz as alterações, retornando o banco ao estado anterior.

### **Eventos que finalizam uma transação:**

✅ **Quando um `COMMIT` ou `ROLLBACK` é emitido explicitamente.**  
✅ **Ao executar um comando DDL (`CREATE`, `ALTER`, `DROP`).**  
✅ **Se o usuário sair do sistema sem confirmar (`COMMIT`) ou cancelar (`ROLLBACK`).**  
✅ **Se houver falha no sistema, ocorre um `ROLLBACK` automático.**

---

**Exemplo: Alterar o departamento de um funcionário e confirmar a transação**

```
SQL> UPDATE emp  
  2  SET deptno = 10  
  3  WHERE empno = 7900;
```

➡️ **Antes do `COMMIT`**, a alteração está apenas na memória.

✅ **Para salvar definitivamente:**

```SQL
COMMIT;
```

✅ **Para desfazer a alteração antes do `COMMIT`:**

```SQL
ROLLBACK;
```

🔹 Se `ROLLBACK` for usado antes do `COMMIT`, **as alterações serão desfeitas**.

![[Pasted image 20250315084422.png]]

**Exemplo do comando rollback:** Excluir todas as linhas da tabela employees

![[Pasted image 20250315084451.png]]

Com o comando Rollback, a alteração provocada é desfeita e a versão original da tabela é restabelecida.

----
👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾
## Consulta com Funções de uma única Linha

É através da linguagem SQL que interagimos com o SGBD. Essa linguagem é composta de categorias de comandos. São elas DDL (comandos de definição de estruturas), DML (comandos de manipulação de dados, DCL (comandos de controle) e DQL (comandos de consulta).

Conhecer os comandos da linguagem SQL é fundamental para acessar o SGBD, manipular estruturas de armazenamento e seus dados.

**Resumo**
É possível realizar operações aritméticas entre os campos de uma tabela dentro do comando Select. Entenda que trata-se apenas de uma consulta, nenhum dado está sendo alterado. Veja o exemplo:

![[Pasted image 20250316074645.png]]

O comando acima calcula o salário anual dos funcionários. Com os Operadores aritméticos podemos realizar expressões aritméticas. Veja o exemplo:

![[Pasted image 20250316074749.png]]

Observe, que nessa consulta, é feito o cálculo do salário anual, o valor do bônus anual que corresponde a 40% do salário anual e o valor total com a soma do salário anual e o bônus.

----

### Consulta com Funções de uma única Linha

É através da linguagem SQL que interagimos com o SGBD. Essa linguagem é composta de categorias de comandos. São elas DDL (comandos de definição de estruturas), DML (comandos de manipulação de dados, DCL (comandos de controle) e DQL (comandos de consulta).

-> Revisando 

É através da linguagem SQL que interagimos com o SGBD. Essa linguagem é composta de categorias de comandos. São elas DDL (comandos de definição de estruturas), DML (comandos de manipulação de dados, DCL (comandos de controle) e DQL (comandos de consulta).
#### 1. DDL (Data Definition Language) - Linguagem de Definição de Dados

Comandos para definir a estrutura do banco de dados (criar, alterar e excluir objetos).

**Exemplos:**
``` SQL
-- Criar uma tabela
CREATE TABLE clientes (
    id INT PRIMARY KEY,
    nome VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    data_cadastro DATE DEFAULT CURRENT_DATE
);

-- Alterar uma tabela (adicionar coluna)
ALTER TABLE clientes ADD COLUMN telefone VARCHAR(20);

-- Excluir uma tabela
DROP TABLE clientes;

-- Criar um índice
CREATE INDEX idx_nome ON clientes(nome);

-- Criar uma view
CREATE VIEW clientes_ativos AS
SELECT * FROM clientes WHERE ativo = TRUE;
```
#### 2. DML (Data Manipulation Language) - Linguagem de Manipulação de Dados

Comandos para manipular os dados armazenados (inserir, atualizar, deletar).

**Exemplos:**

```SQL
-- Inserir dados
INSERT INTO clientes (id, nome, email) 
VALUES (1, 'João Silva', 'joao@email.com');

-- Atualizar dados
UPDATE clientes 
SET telefone = '11999998888' 
WHERE id = 1;

-- Deletar dados
DELETE FROM clientes 
WHERE id = 1;

-- Inserir múltiplos registros
INSERT INTO clientes (id, nome, email) VALUES
(2, 'Maria Souza', 'maria@email.com'),
(3, 'Carlos Lima', 'carlos@email.com');
```

#### 3. DQL (Data Query Language) - Linguagem de Consulta de Dados

Comandos para consultar dados (basicamente o SELECT).

**Exemplos:**

``` SQL
-- Consulta simples
SELECT * FROM clientes;

-- Consulta com filtro
SELECT nome, email FROM clientes 
WHERE data_cadastro > '2023-01-01';

-- Consulta com ordenação
SELECT * FROM clientes 
ORDER BY nome ASC;

-- Consulta com junção de tabelas
SELECT p.descricao, p.preco, c.nome 
FROM produtos p
JOIN clientes c ON p.cliente_id = c.id;

-- Consulta com agregação
SELECT COUNT(*) as total_clientes, 
       AVG(valor_compra) as media_compras
FROM clientes;
```

#### 4. DCL (Data Control Language) - Linguagem de Controle de Dados

Comandos para controlar acesso e permissões.

**Exemplos:**
``` SQL
-- Conceder permissão
GRANT SELECT, INSERT ON clientes TO usuario_app;

-- Revogar permissão
REVOKE DELETE ON clientes FROM usuario_app;

-- Conceder todas as permissões
GRANT ALL PRIVILEGES ON DATABASE meu_banco TO admin;

-- Criar um papel (role) e conceder permissões
CREATE ROLE leitura;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO leitura;
```

## Resumo das categorias:

|Categoria|Propósito|Comandos principais|
|---|---|---|
|DDL|Definir estrutura|CREATE, ALTER, DROP, TRUNCATE, RENAME|
|DML|Manipular dados|INSERT, UPDATE, DELETE, MERGE|
|DQL|Consultar dados|SELECT|
|DCL|Controle de acesso|GRANT, REVOKE, DENY|

Cada tipo de comando tem um propósito específico no gerenciamento e manipulação de bancos de dados relacionais.

### Apelidos (Aliases) em SQL

Os apelidos (ou aliases) em SQL são "apelidos" temporários que você pode atribuir a tabelas ou colunas em suas consultas para tornar o código mais legível ou mais fácil de escrever. Eles são muito úteis em consultas complexas.

### 1. Aliases para Colunas

Usados para renomear colunas nos resultados da consulta.

**Sintaxe:**
```SQL
SELECT 
    nome AS nome_completo,
    email AS endereco_eletronico,
    data_cadastro AS cadastro
FROM clientes;
```

Usados para simplificar referências a tabelas, especialmente em junções.

**Sintaxe:**
```SQL
SELECT 
    c.nome,
    p.descricao
FROM clientes AS c
JOIN pedidos AS p ON c.id = p.cliente_id;
```
1. A palavra-chave `AS` é opcional:
  ```SQL
   SELECT nome nome_completo FROM clientes; -- Funciona igual
   ```

2. Aliases são temporários e só existem durante a execução da consulta.
    
3. São especialmente úteis quando:
    
    - Você tem nomes de colunas longos
  
#### Linguagem SQL e Comandos DDL

É através da linguagem SQL que interagimos com o SGBD. Essa linguagem é composta de categorias de comandos. São elas DDL (comandos de definição de estruturas), DML (comandos de manipulação de dados, DCL (comandos de controle) e DQL (comandos de consulta).

Conhecer os comandos da linguagem SQL é fundamental para acessar o SGBD, manipular estruturas de armazenamento e seus dados.

**DDL – Data Definition Language – Trabalhando Com Tabelas**

A DDL é a parte da SQL usada para criar e manipular objetos que se relacionam aos dados, especialmente tabelas. Com a DDL você pode criar uma tabela, configurar suas colunas e todas as restrições de integridade, por isso antes de começarmos a escrever nossos primeiros comandos temos que entender bem a linguagem SQL e as restrições de integridade envolvidas.

A DDL está intimamente ligada também a modelagem física do banco de dados, pois é nessa parte do projeto onde os modelos lógicos são derivados para um banco de dados real, ou seja, se tornam físicos (saem do papel).

Vamos começar entendendo a sintaxe do comando que é capaz de criar uma tabela, o CREATE TABLE, que funciona da seguinte forma:

![[Pasted image 20250311090907.png]]

Para entender melhor este comando, vamos utilizá-lo em um modelo real. A modelagem conceitual pode ser vista na figura 1, onde estamos criando a base de dados de um pequeno jogo, onde cada personagem é de um tipo e possui um ou mais poderes (somente esta parte do jogo). A figura 2 mostra a derivação do respectivo contexto para a modelagem lógica.

![[Pasted image 20250311092519.png]]

Vamos começar a implementação física deste cenário pela tabela mais simples, ou seja, a que possui menos restrições e não depende de nenhuma outra tabela para existir. Neste caso temos as tabelas “tipo” e “poder”. A tabela “personagem”, por exemplo, possui uma chave estrangeira para “tipo” e, por isso, não poderíamos começar por ela, a não ser que façamos a inclusão da restrição referencial depois, alterando-a.

![[Pasted image 20250311092936.png]]

Repare que assim como na modelagem lógica, a restrição da chave primária recebe um nome, nesse caso “tipo_pk”. Isso ocorre nas restrições de chave e referencial. Ao se incluir a restrição de chave é necessário informar qual é a coluna que recebe essa restrição, neste caso a coluna “idTipo”. Seguindo a mesma lógica, criamos as próximas tabelas.

![[Pasted image 20250311093114.png]]

![[Pasted image 20250311093135.png]]

Repare na criação da tabela “personagem” que há a restrição referencial sendo aplicada com o acréscimo da CONSTRAINT do tipo FOREIGN KEY. Lembre-se que toda restrição, no Oracle, deve ter um nome e, no caso da chave estrangeira, é preciso informar qual coluna local a recebe e qual o “alvo”, ou seja, a tabela e sua respectiva coluna de chave primária.

Por fim, vamos criar a tabela de relacionamento entre “personagem” e “poder”, pois como a relação é N:N (cada personagem pode possuir N poderes e cada poder pode estar associado a N personagens), temos que as relacionar através de uma terceira tabela, conforme:

![[Pasted image 20250311093321.png]]

Repare nas quebras de linhas e a indentação (afastamento da margem) são diferentes para cada comando. Isso quer dizer que não importa se as linhas estão quebradas ou não para a execução do script, mas aqui são descritas assim para maior legibilidade. Essa é, inclusive, uma forte recomendação da comunidade internacional e de qualquer manual de bancos de dados. Repare, ainda, que todos os comandos foram escritos com letras maiúsculas e isso também poderia ter sido diferente, ou seja cada comando poderia ter sido escrito completamente em letras minúsculas, mas por boas práticas de programação escrevemos as palavras reservadas da SQL em letras maiúsculas e o nome dos objetos criados por nós mesmos em letras minúsculas. Por fim, e não menos importante, repare que ao final de cada comando há um “;” que especifica sua finalização.

Se você precisar excluir uma tabela, deve-se utilizar o comando “DROP TABLE nome_da_tabela;”, por exemplo “DROP TABLE tipo;” e a tabela tipo será eliminada do banco de dados. Deve-se utilizar este comando com muito cuidado.

Para se alterar dados de uma tabela, utiliza-se o comando “ALTER TABLE nome_da_tabela MODIFY (modificações);”. A palavra reservada “MODIFY” pode ser substituída por “ADD” se você está adicionando algo na tabela. Por exemplo, se você precisa alterar que a altura do personagem não pode ser nula, deve-se executar o comando “ALTER TABLE personagem MODIFY (altura NOT NULL);” e se você precisar acrescentar uma nova coluna chamada “idade” (que refere-se à idade da personagem), o comando “ALTER TABLE personagem ADD idade NUMBER(2) NULL;” deve ser executado.

Na criação de tabelas, usa-se um comando  DDL. Para criar uma tabela é necessário que o usuário tenha privilégio e uma área para armazenamento. A sintaxe simplificada para criação de tabelas é:


`**Sintaxe: CREATE TABLE** [_esquema._]_tabela_`
          `(nome da coluna _tipo do  dado_ [DEFAULT _expr_]`
              `_[constraint da coluna],_`
              `_...,_`
              `_[constraint da tabela]);_`

onde:

|   |   |
|---|---|
|_Esquema:_|é o  nome do proprietário da tabela, quando omitido a tabela é criada no esquema do usuário corrente|
|_Tabela:_|é o nome da tabela|
|_DEFAULT expr:_|especifica um valor default que será utilizado quando um dado for omitido na inserção|
|_Coluna:_|é o nome da coluna|
|_tipo de dados:_|é o tipo de dados e o comprimento da coluna|
|_Constraint:_|Está cláusula é opcional e especifica as restrições para a coluna ou para a tabela, quando o nome da constraint é omitido o Oracle assume uma identificação|

Convenções para Nomeação de Tabelas e Colunas:

• Deve começar com uma letra

• Pode ter de 1 a 30 caracteres (depende do SGBD)

• Deve conter somente A–Z, a–z, 0–9, _, $ e #

• Não deve duplicar o nome de outro objeto de propriedade do mesmo usuário

• Não deve ser uma palavra reservada pelo Oracle Server

Tipos de Dados:

![[Pasted image 20250311093856.png]]


No exemplo abaixo está sendo criada  a tabela DEPT, com três colunas — chamadas, DEPTNO, DNAME e LOC.

SQL>CREATE TABLE dept  
  2      (deptno NUMBER(2),

  3      dname          VARCHAR2(14),

  4      loc      VARCHAR2(13));

Table created.

A instrução Describe é utilizada para exibir a estrutura de uma tabela.

SQL> DESCRIBE dept

Name                Null?    Type

------------------ -------- ---------

DEPTNO                      NUMBER(2)

DNAME                       VARCHAR2(14)

LOC                         VARCHAR2(13)

---
**Restrições de Integridade**

São elas chaves primárias, chaves estrangeiras, colunas de dados únicos, não nulos etc., especialmente na modelagem lógica. Quando uma restrição é “violada” (não é atendida) é muito mais fácil encontrarmos a origem do erro. Os bancos de dados chamam as restrições com seu termo em inglês, ou seja, “CONSTRAINT”.

As restrições de integridade servem para impedir que dados inválidos sejam inseridos numa determinada coluna e são garantidas pelo próprio SGBD (Sistema Gerenciador de Banco de Dados), nós apenas as configuramos na hora de criar os objetos (através da DDL). Podemos, inclusive, dizer que as restrições (CONSTRAINTS) impõem regras nas colunas. Essas restrições são divididas em seis grupos, sendo:

- Restrição de integridade de **domínio**
- Restrição de integridade de **chave**
- Restrição de integridade **nula**
- Restrição de integridade **referencial**
- Restrição de integridade **unicidade**
- Restrição de integridade **de valor padrão**

A integridade de domínio especifica qual **tipo de valor** um determinado atributo pode admitir, ou seja, é são os tipos de dados (datatypes). Por exemplo, colunas configuradas como número inteiro, número de ponto flutuante, texto, data com hora, somente data, etc. Se um dado do tipo texto for inserido em uma coluna que aceita apenas valores numéricos, a restrição de integridade de domínio será violada. A integridade de domínio pode ir além, podendo **checar** se um valor inserido está dentro de uma especificação. Para isso, utiliza-se a restrição “CHECK”. Por exemplo, o estado no cadastro de um endereço, deve ser uma das 27 opções; o sexo de uma pessoa etc.

A integridade de vazio especifica se o valor de um atributo **pode ou não ser vazio**, ou seja, nulo. São os famosos NULL (permite que um dado seja vazio) e NOT NULL (não permite que um dado não seja especificado naquela coluna na hora de inserir uma linha). A integridade de vazio é também associada à cardinalidade mínima nos relacionamentos (0, a FK pode ser nula. 1, a FK não pode ser nula).

Já a integridade de chave (ou como alguns autores chamam, integridade de chave primária) garante que os valores das chaves primárias sejam sempre únicos e não nulos, pela própria definição de chave primária. Por exemplo, se tentarmos inserir uma linha cuja chave primária já exista, haverá violação da restrição de chave primária.

A integridade referencial é a integridade das FKs (chaves estrangeiras – _Foreign Keys_). Ela garante que o valor que aparecer nos atributos de uma chave estrangeira deve sempre aparecer na chave primária da tabela referenciada, ou seja, garante que todo valor de uma FK seja o mesmo de uma PK, a qual a coluna em questão aponta. Assim sendo, sempre que uma coluna é definida como FK, o SGBD deve garantir que ela sempre aponte para uma PK. Na hora que estamos criando as colunas FKs devemos dizer qual é a tabela alvo e sua respectiva chave primária.

A integridade de unicidade é aquela restrição que permite, ou não, que o valor se repita. No banco de dados utilizamos a palavra reservada UNIQUE quando queremos que seus dados sejam únicos, como por exemplo, o RG de uma pessoa, o e-mail de um usuário, os dados de uma impressão digital etc. Não confunda a restrição de unicidade com a de chave primária, pois os valores dessa coluna não são necessariamente identificadores da tabela.

Por fim e não menos importante temos a integridade de valor padrão associada à palavra reservada DEFAULT. Essa restrição permite que se um valor nulo for inserido em uma coluna (ou não foi informado, por exemplo) um valor padrão (pré-definido) é colocado em seu lugar. Por exemplo, se o país não foi informado numa tabela de endereços incluir “Brasil”. Essa restrição está fortemente ligada à restrição de nulo.

É muito importante reforçar que todas as restrições de integridade são garantidas pelo próprio SGBD. Uma restrição que não se encaixa em nenhuma das citadas aqui é chamada de restrição semântica e deve ser garantida pelo software que utiliza o banco de dados. Por exemplo, a cardinalidade máxima de um relacionamento ou, ainda como exemplo real, imagine que temos um relacionamento entre funcionários e departamento, onde um funcionário de recursos humanos não poderia assumir o cargo de analista de sistemas. Essa é uma restrição que deve ser garantida pela própria aplicação.

Pockt Guide

![[Pasted image 20250311095133.png]]

![[Pasted image 20250311095202.png]]

----

# Comandos DML  e DQL

**Introdução** 

É através da linguagem SQL que interagimos com o SGBD. Essa linguagem é composta de categorias de comandos. São elas DDL (comandos de definição de estruturas), DML (comandos de manipulação de dados, DCL (comandos de controle) e DQL (comandos de consulta).

Conhecer os comandos da linguagem SQL é fundamental para acessar o SGBD, manipular estruturas de armazenamento e seus dados.

**Comandos DML**

Os comandos da categoria DML (Data Manipulation Language), servem para realizar  adições, eliminações e atualizações em dados de um ou mais registros de uma ou mais tabelas de maneira concorrente. Os comandos da categoria DML são:

- Insert – Adição de linhas com  dados na tabela
- Update – Atualização de  dados na tabela
- Delete – Eliminação de dados da tabela
- Commit – Confirmação das transações, ou seja, salvamento dos dados
- Rollback – Desistência das transações, ou seja, desfazer a última transação

**A adição de linhas com dados é um comando DML.**

**Sintaxe:**

**INSERT INTO** _tabela_ [(_coluna_ [_, coluna..._])] **VALUES** _(valor_ [_, valor..._])_;_

Onde:

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1693227350131-XB2TF5sprq.png)


### **Verificando a estrutura de uma tabela**

Para visualizar a ordem padrão das colunas e os tipos de dados esperados, utilize o comando `DESCRIBE`:

```
SQL> DESCRIBE dept;
```

📌 **Saída do comando:**

|Nome da Coluna|Permite Nulo?|Tipo de Dado|
|---|---|---|
|**DEPTNO**|NOT NULL|NUMBER(2)|
|**DNAME**|NULL|VARCHAR2(14)|
|**LOC**|NULL|VARCHAR2(13)|

🔹 O comando `DESCRIBE` exibe:

- A **ordem das colunas** na tabela.
- Se a coluna aceita valores **NULL**.
- O **tipo de dado** definido para cada campo.

💡 **Dica:** Sempre use `DESCRIBE` antes de inserir dados para garantir que os valores inseridos correspondam ao tipo esperado.


**Exemplo 1: Inserção completa com colunas especificadas**

```
SQL> INSERT INTO dept (DEPTNO, DNAME, LOC)  
  2  VALUES (80, 'COMERCIAL', 'SP');
```

🔹 Neste exemplo, estamos inserindo um novo departamento (**DEPTNO 80**) chamado **"COMERCIAL"**, localizado em **"SP"**.


**Exemplo 2: Inserção sem especificar colunas (assumindo a ordem da tabela)**

```
SQL> INSERT INTO dept  
  2  VALUES (90, 'FINANCEIRO', 'RJ');
```

🔹 Aqui, os valores estão sendo inseridos diretamente, assumindo que a tabela **`dept`** possui exatamente três colunas na ordem correta (**DEPTNO, DNAME e LOC**).

📌 **Recomendação:** Sempre que possível, especifique os nomes das colunas para evitar problemas caso a estrutura da tabela mude no futuro.

### **Inserção de Dados em Tabelas**


**Exemplo 3: Inserção parcial de dados**

```
SQL> INSERT INTO dept (deptno, dname)  
  2  VALUES (55, 'RH');
```

🔹 A tabela **`dept`** contém as colunas **`deptno`**, **`dname`** e **`loc`**.  
🔹 Como o campo **`loc`** não foi especificado, ele será preenchido automaticamente com **NULL**.


**Exemplo 4: Inserção com valor NULL explícito**

```
SQL> INSERT INTO dept  
  2  VALUES (45, 'DIRETORIA', NULL);
```

🔹 Aqui, os valores estão sendo inseridos diretamente, e o campo **`loc`** recebe **NULL** explicitamente.  
🔹 Isso é útil quando queremos deixar claro que o campo não terá um valor atribuído.


## **Inserção de Dados com Datas**

 **Exemplo 5: Inserindo um registro na tabela `emp`**

```
SQL> INSERT INTO emp  
  2  VALUES (3000, 'JOSE', 'VENDEDOR', 7782, TO_DATE('30/03/23', 'DD/MM/YY'),  
  3          2800, NULL, 20);
```

🔹 **Explicação dos valores inseridos:**

- `3000` → Código do empregado.
- `'JOSE'` → Nome do empregado.
- `'VENDEDOR'` → Cargo.
- `7782` → Código do gerente.
- `TO_DATE('30/03/23', 'DD/MM/YY')` → Data de admissão (convertida para formato de data).
- `2800` → Salário.
- `NULL` → Comissão (não aplicável).
- `20` → Código do departamento.

### **Visualizando os dados inseridos:**

Para verificar os registros na tabela **`emp`**, use:

```
SQL> SELECT *  
  2  FROM emp;
```

## **Atualização de Dados nos Registros**

**Sintaxe do comando `UPDATE`**

```
UPDATE tabela  
SET coluna = valor [, coluna = valor, ...]  
[WHERE condição];  
```

🔹 **Importante:** Se a cláusula `WHERE` for omitida, **todas as linhas** da tabela serão alteradas!

### **Exemplo: Atualizando um registro específico**

Atualizar o departamento para **30** do empregado com código **7900**:

```
SQL> UPDATE emp  
  2  SET deptno = 30  
  3  WHERE empno = 7900;
```

📌 **Sempre utilize a cláusula `WHERE` ao atualizar registros para evitar modificar toda a tabela por engano.**

### **Comando `SELECT`**

O comando `SELECT` é utilizado para realizar consultas aos dados armazenados em uma tabela.

**Exemplo de `SELECT` exibindo todos os dados da tabela `emp`**

```
SQL> SELECT *  
  2  FROM emp;
```

🔹 O asterisco (`*`) indica que **todas as colunas** da tabela serão retornadas na consulta.

## **Sintaxe do Comando `SELECT`**

🔹 **Regras para uso dos comandos SQL:**

- O SQL **não diferencia maiúsculas e minúsculas** no processamento dos comandos.
- Os comandos podem ser escritos em **uma ou mais linhas**.
- **Não é permitido abreviar** as palavras-chave dos comandos.
- **Escrever cada parte do comando em uma linha separada** melhora a legibilidade.
- Para exibir **apenas colunas específicas**, devemos nomeá-las na consulta.

 **Exemplo: Exibir apenas algumas colunas**
```
SQL> SELECT deptno, dname  
  2  FROM dept;
```

🔹 Aqui, estamos consultando apenas as colunas **`deptno`** (número do departamento) e **`dname`** (nome do departamento).

# **Operadores Aritméticos**

Os operadores aritméticos podem ser utilizados em qualquer cláusula de uma instrução SQL, **exceto na cláusula `FROM`**.

![[Pasted image 20250315082302.png]]

 **Exemplo: Exibir o salário original e o salário acrescido de R$ 300,00**

``` SQL
SQL> SELECT ename, sal, sal + 300  
  2  FROM emp;
```

![[Pasted image 20250315082338.png]]
➡️ **Nova coluna gerada apenas para exibição:** O resultado apresentará os nomes dos empregados (**`ename`**), seus salários originais (**`sal`**) e uma **coluna extra** mostrando os salários com um acréscimo de R$ 300,00.

### **Ordem de precedência matemática**

As regras matemáticas e a ordem de precedência continuam válidas dentro do SQL.

``` SQL
 SQL> SELECT ename, sal, sal + ((sal * 30) / 100)  
  2  FROM emp;
```

➡️ Aqui, estamos calculando o salário acrescido de **30%**.

✅ **Dica:** Use **parênteses** para garantir a ordem correta dos cálculos.

# **Operadores de Comparação**

Os operadores de comparação são utilizados para **estabelecer relações entre valores ou expressões**.

- O resultado de uma comparação é sempre um valor **booleano** (`TRUE` ou `FALSE`).
- Podem ser usados em **comparações que envolvem apenas uma linha**.

![[Pasted image 20250315082444.png]]

### **Operador `BETWEEN`**

Os valores especificados com `BETWEEN` são **inclusivos**. O limite **inferior** deve ser especificado primeiro.

```SQL
SQL> SELECT ename, sal  
  2  FROM emp  
  3  WHERE sal BETWEEN 1000 AND 1500;
```

➡️ Retorna os funcionários cujo salário está **entre R$ 1.000 e R$ 1.500** (inclusive).

### **Operador `IN`**

Verifica se um valor está presente em uma **lista de valores específicos**.

```SQL
SQL> SELECT empno, ename, mgr, deptno  
  2  FROM emp  
  3  WHERE ename IN ('FORD', 'ALLEN');
```

➡️ Retorna os funcionários cujo nome seja **"FORD"** ou **"ALLEN"**.

✅ Se forem utilizados **caracteres ou datas**, eles devem estar entre **aspas simples (`'`)**:

```SQL
SQL> SELECT empno, ename, mgr, deptno  
  2  FROM scott.emp  
  3  WHERE job IN ('PRESIDENT', 'MANAGER');
```

➡️ Retorna funcionários cujo cargo (`job`) seja **"PRESIDENT"** ou **"MANAGER"**.

### **Operador `LIKE`**

O operador `LIKE` permite buscar registros que **correspondam a um padrão de caracteres**.

```SQL 
SQL> SELECT ename  
  2  FROM scott.emp  
  3  WHERE ename LIKE 'J%';
```

➡️ Retorna todos os funcionários cujo nome começa com **"J"** (letra maiúscula).  
🔹 Se houver nomes iniciados com **"j" minúsculo**, eles **não serão retornados**.

✅ **Símbolos utilizados no `LIKE`**:

- `%` → Representa **qualquer sequência de caracteres**.
    - Exemplo: `'A%'` encontra **"Ana"**, **"Antonio"**, **"Alberto"**, etc.
- `_` → Representa **um único caractere**.
    - Exemplo: `'A_'` encontra **"Ao"**, **"An"**, mas não **"Ana"**.

---

### **Operador `IS NULL`**

Usado para verificar campos que **não possuem valor** (`NULL`).

```SQL
SQL> SELECT ename, job, deptno  
  2  FROM scott.emp  
  3  WHERE comm IS NULL;
```

➡️ Retorna os funcionários que **não recebem comissão** (`comm` está `NULL`).

✅ **Importante:** `NULL` significa **ausência de valor**.  
❌ **Não podemos usar `=` ou `!=` para comparar valores `NULL`**, pois `NULL` **não é igual nem diferente de nada**.

# **Operadores Lógicos**

Os operadores lógicos permitem combinar múltiplas condições para gerar um **único resultado**.  
✅ **Principais operadores lógicos no SQL:**

1. **`AND`** → Ambas as condições devem ser **verdadeiras**.
2. **`OR`** → Pelo menos **uma** das condições deve ser verdadeira.
3. **`NOT`** → Inverte o resultado da condição.

 **Exemplo: Filtrar funcionários com salário maior que 2000 e que pertencem ao departamento 30**

```SQL
SQL> SELECT ename, sal, deptno  
  2  FROM emp  
  3  WHERE sal > 2000 AND deptno = 30;
```

➡️ Apenas os funcionários do **departamento 30** com **salário superior a R$ 2.000** serão retornados.

# **Operadores Lógicos no SQL**

Os operadores lógicos são utilizados para **combinar expressões** na cláusula `WHERE`. Eles podem ser aplicados em **consultas (`SELECT`)**, **atualizações (`UPDATE`)** e **exclusões (`DELETE`)** de dados.

## **Operador `AND`**

O operador `AND` retorna resultados **apenas quando todas as condições são verdadeiras**.

**Exemplo: Selecionar funcionários com salário ≥ 1100 e cargo `SALESMAN`**

```SQL
SQL> SELECT empno, ename, job, sal  
  2  FROM scott.emp  
  3  WHERE sal >= 1100 AND job = 'SALESMAN';
```

✅ **Resultado:**

``` 
EMPNO     ENAME      JOB        SAL  
7876      ADAMS      SALESMAN   1100  
7934      MILLER     SALESMAN   1300  
```

- Apenas os funcionários que atendem **ambas as condições** (`sal >= 1100` **E** `job = 'SALESMAN'`) são selecionados.
- Se qualquer condição for **falsa**, a linha não será incluída no resultado.

⚠️ **Cuidado com maiúsculas e minúsculas em valores alfanuméricos!**

- SQL **distingue letras maiúsculas e minúsculas**. No exemplo acima, `SALESMAN` deve estar em **maiúsculas**, caso contrário, nenhum resultado será retornado.

## **Operador `OR`**

O operador `OR` retorna resultados **quando pelo menos uma das condições for verdadeira**.

**Exemplo: Selecionar funcionários com salário ≥ 1100 ou cargo `SALESMAN`**

``` SQL
 SELECT empno, ename, job, sal  
  2  FROM emp  
  3  WHERE sal >= 1100 OR job = 'SALESMAN';
```

✅ **Resultado (parcial):**

```
EMPNO     ENAME     JOB         SAL  
7839      KING      PRESIDENT   5000  
7698      BLAKE     MANAGER     2850  
7782      CLARK     MANAGER     2450  
7566      JONES     MANAGER     2975  
7654      MARTIN    SALESMAN    1250  
...
```

- Se um funcionário **tiver salário ≥ 1100** **OU** **for `SALESMAN`**, ele será incluído no resultado.
- Funcionários que atendem **apenas uma das condições** também aparecem na consulta.

## **Operador `NOT`**

O operador `NOT` **inverte o resultado de uma condição**.

### **Exemplo: Selecionar funcionários que NÃO sejam `CLERK`, `MANAGER` ou `ANALYST`**

```
SQL> SELECT ename, job  
  2  FROM scott.emp  
  3  WHERE job NOT IN ('CLERK', 'MANAGER', 'ANALYST');
```

✅ **Resultado:**

```
ENAME      JOB  
KING       PRESIDENT  
MARTIN     SALESMAN  
ALLEN      SALESMAN  
TURNER     SALESMAN  
WARD       SALESMAN  
```

- **Apenas os funcionários que NÃO possuem os cargos listados** (`CLERK`, `MANAGER`, `ANALYST`) aparecem no resultado.

✅ **`NOT` pode ser combinado com outros operadores:**

```
... WHERE job   NOT IN ('SALESMAN', 'MANAGER');  -- Exclui SALESMAN e MANAGER  
... WHERE sal   NOT BETWEEN 2500 AND 5000;      -- Exclui salários entre 2500 e 5000  
... WHERE ename NOT LIKE '%S%';                 -- Exclui nomes que contenham "S"  
... WHERE comm  IS   NOT NULL;                  -- Seleciona funcionários com comissão  
```

# **Controle de Transações (COMMIT & ROLLBACK)**

As transações garantem que um conjunto de operações **DML** (`INSERT`, `UPDATE`, `DELETE`) seja executado corretamente no banco de dados.

### **Requisitos das transações:**

✔ **Consistência** → Os dados devem permanecer íntegros.  
✔ **Atomicidade** → Todas as operações devem ser concluídas com sucesso ou nenhuma será realizada.  
✔ **Integridade** → O banco de dados deve sempre manter um estado válido.

🚀 **Exemplo prático: Transferência de dinheiro**

1. Debita um valor da conta A (`UPDATE` na conta de origem).
2. Credita o mesmo valor na conta B (`UPDATE` na conta de destino).
3. **Se ambos os passos forem bem-sucedidos**, a transação é **confirmada (`COMMIT`)**.
4. **Se houver erro**, a transação é **desfeita (`ROLLBACK`)**.

---

## **COMMIT & ROLLBACK**

📌 **COMMIT** → Confirma as alterações no banco de dados de forma permanente.  
📌 **ROLLBACK** → Desfaz as alterações, retornando o banco ao estado anterior.

### **Eventos que finalizam uma transação:**

✅ **Quando um `COMMIT` ou `ROLLBACK` é emitido explicitamente.**  
✅ **Ao executar um comando DDL (`CREATE`, `ALTER`, `DROP`).**  
✅ **Se o usuário sair do sistema sem confirmar (`COMMIT`) ou cancelar (`ROLLBACK`).**  
✅ **Se houver falha no sistema, ocorre um `ROLLBACK` automático.**

---

**Exemplo: Alterar o departamento de um funcionário e confirmar a transação**

```
SQL> UPDATE emp  
  2  SET deptno = 10  
  3  WHERE empno = 7900;
```

➡️ **Antes do `COMMIT`**, a alteração está apenas na memória.

✅ **Para salvar definitivamente:**

```SQL
COMMIT;
```

✅ **Para desfazer a alteração antes do `COMMIT`:**

```SQL
ROLLBACK;
```

🔹 Se `ROLLBACK` for usado antes do `COMMIT`, **as alterações serão desfeitas**.

![[Pasted image 20250315084422.png]]

**Exemplo do comando rollback:** Excluir todas as linhas da tabela employees

![[Pasted image 20250315084451.png]]

Com o comando Rollback, a alteração provocada é desfeita e a versão original da tabela é restabelecida.

----
👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾
## Consulta com Funções de uma única Linha

É através da linguagem SQL que interagimos com o SGBD. Essa linguagem é composta de categorias de comandos. São elas DDL (comandos de definição de estruturas), DML (comandos de manipulação de dados, DCL (comandos de controle) e DQL (comandos de consulta).

Conhecer os comandos da linguagem SQL é fundamental para acessar o SGBD, manipular estruturas de armazenamento e seus dados.

**Resumo**
É possível realizar operações aritméticas entre os campos de uma tabela dentro do comando Select. Entenda que trata-se apenas de uma consulta, nenhum dado está sendo alterado. Veja o exemplo:

![[Pasted image 20250316074645.png]]

O comando acima calcula o salário anual dos funcionários. Com os Operadores aritméticos podemos realizar expressões aritméticas. Veja o exemplo:

![[Pasted image 20250316074749.png]]

Observe, que nessa consulta, é feito o cálculo do salário anual, o valor do bônus anual que corresponde a 40% do salário anual e o valor total com a soma do salário anual e o bônus.

----

### Consulta com Funções de uma única Linha

É através da linguagem SQL que interagimos com o SGBD. Essa linguagem é composta de categorias de comandos. São elas DDL (comandos de definição de estruturas), DML (comandos de manipulação de dados, DCL (comandos de controle) e DQL (comandos de consulta).

-> Revisando 

É através da linguagem SQL que interagimos com o SGBD. Essa linguagem é composta de categorias de comandos. São elas DDL (comandos de definição de estruturas), DML (comandos de manipulação de dados, DCL (comandos de controle) e DQL (comandos de consulta).
#### 1. DDL (Data Definition Language) - Linguagem de Definição de Dados

Comandos para definir a estrutura do banco de dados (criar, alterar e excluir objetos).

**Exemplos:**
``` SQL
-- Criar uma tabela
CREATE TABLE clientes (
    id INT PRIMARY KEY,
    nome VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    data_cadastro DATE DEFAULT CURRENT_DATE
);

-- Alterar uma tabela (adicionar coluna)
ALTER TABLE clientes ADD COLUMN telefone VARCHAR(20);

-- Excluir uma tabela
DROP TABLE clientes;

-- Criar um índice
CREATE INDEX idx_nome ON clientes(nome);

-- Criar uma view
CREATE VIEW clientes_ativos AS
SELECT * FROM clientes WHERE ativo = TRUE;
```
#### 2. DML (Data Manipulation Language) - Linguagem de Manipulação de Dados

Comandos para manipular os dados armazenados (inserir, atualizar, deletar).

**Exemplos:**

```SQL
-- Inserir dados
INSERT INTO clientes (id, nome, email) 
VALUES (1, 'João Silva', 'joao@email.com');

-- Atualizar dados
UPDATE clientes 
SET telefone = '11999998888' 
WHERE id = 1;

-- Deletar dados
DELETE FROM clientes 
WHERE id = 1;

-- Inserir múltiplos registros
INSERT INTO clientes (id, nome, email) VALUES
(2, 'Maria Souza', 'maria@email.com'),
(3, 'Carlos Lima', 'carlos@email.com');
```

#### 3. DQL (Data Query Language) - Linguagem de Consulta de Dados

Comandos para consultar dados (basicamente o SELECT).

**Exemplos:**

``` SQL
-- Consulta simples
SELECT * FROM clientes;

-- Consulta com filtro
SELECT nome, email FROM clientes 
WHERE data_cadastro > '2023-01-01';

-- Consulta com ordenação
SELECT * FROM clientes 
ORDER BY nome ASC;

-- Consulta com junção de tabelas
SELECT p.descricao, p.preco, c.nome 
FROM produtos p
JOIN clientes c ON p.cliente_id = c.id;

-- Consulta com agregação
SELECT COUNT(*) as total_clientes, 
       AVG(valor_compra) as media_compras
FROM clientes;
```

#### 4. DCL (Data Control Language) - Linguagem de Controle de Dados

Comandos para controlar acesso e permissões.

**Exemplos:**
``` SQL
-- Conceder permissão
GRANT SELECT, INSERT ON clientes TO usuario_app;

-- Revogar permissão
REVOKE DELETE ON clientes FROM usuario_app;

-- Conceder todas as permissões
GRANT ALL PRIVILEGES ON DATABASE meu_banco TO admin;

-- Criar um papel (role) e conceder permissões
CREATE ROLE leitura;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO leitura;
```

## Resumo das categorias:

|Categoria|Propósito|Comandos principais|
|---|---|---|
|DDL|Definir estrutura|CREATE, ALTER, DROP, TRUNCATE, RENAME|
|DML|Manipular dados|INSERT, UPDATE, DELETE, MERGE|
|DQL|Consultar dados|SELECT|
|DCL|Controle de acesso|GRANT, REVOKE, DENY|

Cada tipo de comando tem um propósito específico no gerenciamento e manipulação de bancos de dados relacionais.

### Apelidos (Aliases) em SQL

Os apelidos (ou aliases) em SQL são "apelidos" temporários que você pode atribuir a tabelas ou colunas em suas consultas para tornar o código mais legível ou mais fácil de escrever. Eles são muito úteis em consultas complexas.

### 1. Aliases para Colunas

Usados para renomear colunas nos resultados da consulta.

**Sintaxe:**
```SQL
SELECT 
    nome AS nome_completo,
    email AS endereco_eletronico,
    data_cadastro AS cadastro
FROM clientes;
```

Usados para simplificar referências a tabelas, especialmente em junções.

**Sintaxe:**
```SQL
SELECT 
    c.nome,
    p.descricao
FROM clientes AS c
JOIN pedidos AS p ON c.id = p.cliente_id;
```

1. A palavra-chave `AS` é opcional:
  ```SQL
   SELECT nome nome_completo FROM clientes; -- Funciona igual
   ```
   
2. Aliases são temporários e só existem durante a execução da consulta.
    
3. São especialmente úteis quando:
    
    - Você tem nomes de colunas longos
  
    - Trabalha com múltiplas tabelas
    
    - Usa funções ou expressões nas colunas
    
    - Há colunas com nomes iguais em tabelas diferentes
    
4. Para apelidos que contenham espaços ou caracteres especiais, use aspas:
```SQL
SELECT nome AS "Nome Completo" FROM clientes;
```

## Exemplos avançados:

**Com funções:**
```SQL
SELECT 
    AVG(salario) AS media_salarial,
    COUNT(*) AS total_funcionarios
FROM empregados;
```

**Com expressões:**
```SQL
SELECT 
    nome || ' ' || sobrenome AS nome_completo,
    salario * 12 AS salario_anual
FROM funcionarios;
```

➡️ versão alternativa com MySQL
```MySQL
SELECT 
    CONCAT(nome, ' ', sobrenome) AS nome_completo,
    salario * 12 AS salario_anual
FROM funcionarios;
```

**Com múltiplas tabelas (muito comum):**
```SQL
SELECT 
    p.nome AS produto,
    f.nome AS fabricante,
    p.preco AS preco_unitario
FROM produtos AS p
JOIN fabricantes AS f ON p.fabricante_id = f.id;
```

**Em subconsultas:**
```SQL
SELECT 
    d.nome AS departamento,
    sub.media AS media_salarial
FROM departamentos d
JOIN (
    SELECT 
        departamento_id, 
        AVG(salario) AS media
    FROM empregados
    GROUP BY departamento_id
) AS sub ON d.id = sub.departamento_id;
```

Os aliases são uma ferramenta poderosa para tornar suas consultas SQL mais claras e fáceis de manter, especialmente em consultas complexas com múltiplas tabelas e junções.

### **Funções de Linha Única (Single-Row Functions) em SQL**
As **funções de linha única** são funções SQL que operam em **cada registro individualmente**, retornando um resultado para cada linha processada. Elas são aplicadas a **valores de colunas** e podem ser usadas em consultas `SELECT`, `WHERE`, `ORDER BY` e outras cláusulas.

## **Categorias de Funções de Linha Única**

### **1. Funções de Texto (String Functions)**

Manipulam dados do tipo **CHAR, VARCHAR, TEXT**.

|Função|Descrição|Exemplo|Resultado|
|---|---|---|---|
|`UPPER(texto)`|Converte para maiúsculas|`UPPER('sql')`|`SQL`|
|`LOWER(texto)`|Converte para minúsculas|`LOWER('SQL')`|`sql`|
|`INITCAP(texto)`|Primeira letra maiúscula (Oracle, PostgreSQL)|`INITCAP('sql server')`|`Sql Server`|
|`LENGTH(texto)`|Retorna o tamanho do texto|`LENGTH('Banco de Dados')`|`13`|
|`SUBSTR(texto, start, length)`|Extrai parte de uma string|`SUBSTR('SQL Server', 5, 6)`|`Server`|
|`REPLACE(texto, old, new)`|Substitui parte de uma string|`REPLACE('SQL Server', 'SQL', 'MySQL')`|`MySQL Server`|
|`CONCAT(str1, str2)`|Concatena strings|`CONCAT('SQL', ' Server')`|`SQL Server`|
|`TRIM(texto)`|Remove espaços em branco no início e no fim|`TRIM(' SQL ')`|`SQL`|

---

### **2. Funções Numéricas (Numeric Functions)**

Operam em valores **INT, FLOAT, DECIMAL**.

|Função|Descrição|Exemplo|Resultado|
|---|---|---|---|
|`ROUND(num, dec)`|Arredonda um número|`ROUND(15.78, 1)`|`15.8`|
|`TRUNC(num, dec)`|Trunca (corta) casas decimais|`TRUNC(15.78, 1)`|`15.7`|
|`CEIL(num)`|Arredonda para cima (menor inteiro >= num)|`CEIL(15.2)`|`16`|
|`FLOOR(num)`|Arredonda para baixo (maior inteiro <= num)|`FLOOR(15.9)`|`15`|
|`MOD(num1, num2)`|Retorna o resto da divisão|`MOD(10, 3)`|`1`|
|`ABS(num)`|Retorna o valor absoluto|`ABS(-15)`|`15`|
|`POWER(num, exp)`|Eleva um número a uma potência|`POWER(2, 3)`|`8`|

---

### **3. Funções de Data (Date Functions)**

Manipulam valores **DATE, TIMESTAMP**.

|Função|Descrição|Exemplo (Oracle)|Resultado|
|---|---|---|---|
|`SYSDATE` / `NOW()`|Retorna a data e hora atuais|`SELECT SYSDATE FROM dual;`|`2023-10-25 14:30:00`|
|`TO_CHAR(data, formato)`|Converte data para texto formatado|`TO_CHAR(SYSDATE, 'DD/MM/YYYY')`|`25/10/2023`|
|`TO_DATE(texto, formato)`|Converte texto para data|`TO_DATE('25-10-2023', 'DD-MM-YYYY')`|`2023-10-25`|
|`MONTHS_BETWEEN(data1, data2)`|Calcula meses entre duas datas (Oracle)|`MONTHS_BETWEEN('25-OCT-2023', '25-JAN-2023')`|`9`|
|`ADD_MONTHS(data, meses)`|Adiciona meses a uma data (Oracle)|`ADD_MONTHS(SYSDATE, 3)`|`2024-01-25`|
|`LAST_DAY(data)`|Retorna o último dia do mês|`LAST_DAY(SYSDATE)`|`2023-10-31`|

---

### **4. Funções de Conversão (Conversion Functions)**

Convertem um tipo de dado em outro.

|Função|Descrição|Exemplo|Resultado|
|---|---|---|---|
|`TO_CHAR(num/data)`|Converte número/data para texto|`TO_CHAR(1500, '$9999')`|`$1500`|
|`TO_NUMBER(texto)`|Converte texto para número|`TO_NUMBER('1500')`|`1500`|
|`CAST(valor AS tipo)`|Conversão genérica|`CAST('2023-10-25' AS DATE)`|`2023-10-25`|

---

### **5. Funções Condicionais (Conditional Functions)**

Retornam valores com base em condições.

|Função|Descrição|Exemplo (Oracle)|Resultado|
|---|---|---|---|
|`NVL(valor, substituto)`|Se `valor` for NULL, retorna `substituto`|`NVL(salario, 0)`|`0` (se salario for NULL)|
|`COALESCE(val1, val2, ...)`|Retorna o primeiro valor não-NULL|`COALESCE(telefone, celular, 'Sem contato')`|`'Sem contato'` (se ambos forem NULL)|
|`DECODE` (Oracle) / `CASE`|Estrutura condicional|`CASE WHEN salario > 5000 THEN 'Alto' ELSE 'Baixo' END`|`'Alto'` ou `'Baixo'`|

---
**Exemplo:**
```SQL
SELECT 
    nome,
    UPPER(sobrenome) AS sobrenome_maiusculo,
    salario,
    ROUND(salario * 1.10, 2) AS salario_com_aumento,
    TO_CHAR(data_contratacao, 'DD/MM/YYYY') AS data_formatada,
    NVL(telefone, 'Não informado') AS telefone
FROM funcionarios
WHERE LENGTH(nome) > 5
ORDER BY salario DESC;
```

**Resultado:**

|nome|sobrenome_maiusculo|salario|salario_com_aumento|data_formatada|telefone|
|---|---|---|---|---|---|
|João|SILVA|5000|5500.00|15/03/2020|(11) 9999-8888|
|Maria|SANTOS|4500|4950.00|20/05/2021|Não informado|

# **Funções de Conversão de Data em SQL**

As funções de conversão de data são essenciais para manipular e formatar valores temporais em bancos de dados. Elas permitem transformar:

- **Strings em datas** (para armazenamento ou filtro)
    
- **Datas em strings** (para exibição amigável)
    
- **Entre formatos de data/hora** (timestamp → date, etc.)

##### **Principais funções:**

**`MONTHS_BETWEEN(data1, data2)`**  
Calcula o número de meses entre duas datas (pode retornar valor fracionário).
```SQL
SELECT MONTHS_BETWEEN('15-JAN-2025', '15-MAR-2024') FROM dual;
-- Retorno: 10 (meses entre as datas)
```

**`ADD_MONTHS(data, n)`**  
Adiciona ou subtrai meses a uma data.
```SQL
SELECT ADD_MONTHS('01-JAN-2024', 3) FROM dual;
-- Retorno: 01-APR-2024
```

**`LAST_DAY(data)`**  
Retorna o último dia do mês da data especificada.
```SQL
SELECT LAST_DAY('10-FEB-2024') FROM dual;
-- Retorno: 29-FEB-2024 (2024 é bissexto)
```

**`NEXT_DAY(data, 'dia_semana')`**  
Encontra a próxima ocorrência de um dia da semana após a data.
```SQL
SELECT NEXT_DAY('01-MAR-2024', 'SEGUNDA') FROM dual;
-- Retorno: 04-MAR-2024 (próxima segunda-feira)
```

#### Funções para Conversão de Dados**

### **Principais funções:**

**`TO_CHAR(data|número, formato)`**  
Converte datas ou números para texto formatado.
```SQL
SELECT TO_CHAR(SYSDATE, 'DD/MM/YYYY HH24:MI') FROM dual;
-- Retorno: "24/03/2024 14:30"
```

**`TO_DATE(texto, formato)`**  
Converte texto em data.
```SQL
SELECT TO_DATE('25-Dez-2024', 'DD-Mon-YYYY') FROM dual;
-- Retorno: 25/12/2024 (como valor DATE)
```

**`TO_NUMBER(texto, formato)`**  
Converte texto em número.
```SQL
SELECT TO_NUMBER('1.250,50', '9G999D99') FROM dual;
-- Retorno: 1250.5 (como valor numérico)
```

#### **Conversão de Datas em Caracteres**

**Formatos mais usados com TO_CHAR:**

|Código|Descrição|Exemplo de Saída|
|---|---|---|
|`DD`|Dia do mês (01-31)|15|
|`MM`|Mês (01-12)|03|
|`YYYY`|Ano com 4 dígitos|2024|
|`DAY`|Nome completo do dia|"SEGUNDA-FEIRA"|
|`MON`|Nome abreviado do mês|"MAR"|
|`HH24`|Hora no formato 24h|14|
|`MI`|Minutos|30|

#### **Função NVL**
Substitui valores NULL por um valor padrão especificado.

**Sintaxe:**
```SQL
NVL(valor, valor_se_null)
```

**Casos de uso:**
1. Evitar erros em cálculos com NULL
2. Melhorar a apresentação de dados em relatórios

**Exemplos:**
Substituição de NULL por 0 em comissões
```SQL
-- Substituir NULL por 0 em comissões
SELECT 
    nome,
    salario,
    NVL(comissao, 0) AS comissao_ajustada,
    salario + NVL(comissao, 0) AS total
FROM vendedores;

-- Substituir NULL por texto
SELECT 
    nome,
    NVL(email, 'E-mail não cadastrado') AS contato
FROM clientes;
```

**Resultado (tabela fictícia):**

|NOME|SALARIO|COMISSAO_AJUSTADA|TOTAL|
|---|---|---|---|
|João|2500|300|2800|
|Maria|1800|0|1800|
|Carlos|2200|150|2350|
|Ana|3000|500|3500|
|Pedro|2000|0|2000|

**Observação:** Maria e Pedro tinham NULL na coluna comissao, que foram substituídos por 0.

Substituição de NULL por texto
```SQL
SELECT 
    nome,
    NVL(email, 'E-mail não cadastrado') AS contato
FROM clientes;
```

**Resultado (tabela fictícia):**

|NOME|CONTATO|
|---|---|
|Ana|[ana@empresa.com](https://mailto:ana@empresa.com/)|
|Luiz|E-mail não cadastrado|
|Carla|[carla.silva@email.com](https://mailto:carla.silva@email.com/)|
|Marcos|E-mail não cadastrado|
|Fernanda|[fernanda@outlook.com](https://mailto:fernanda@outlook.com/)|
**Observação:** Luiz e Marcos tinham NULL na coluna email, que foram substituídos pelo texto padrão.

 
 Exemplo com COALESCE
 ```SQL
 SELECT 
    nome,
    COALESCE(comissao, bonus, 0) AS remuneracao_variavel
FROM vendedores;
```

**Resultado (tabela fictícia):**

|NOME|REMUNERACAO_VARIAVEL|
|---|---|
|João|300|
|Maria|100|
|Carlos|150|
|Ana|500|
|Pedro|0|

**Observação:**

- João, Carlos e Ana tinham valores em 'comissao'
    
- Maria tinha NULL em 'comissao' mas 100 em 'bonus'
    
- Pedro tinha NULL em ambas colunas, retornando 0
    

## Diferença entre NVL e COALESCE

|Função|Vantagens|Limitações|
|---|---|---|
|NVL|Simples, presente em todos os bancos|Só trabalha com 2 argumentos|
|COALESCE|Aceita múltiplos argumentos|Não suportado em bancos muito antigos|

COALESCE é particularmente útil quando você tem várias colunas alternativas que podem conter valores nulos.

# extra
questões 
```SQL
SELECT TO_CHAR(price, '$999990.99')
FROM inventory;
```

- `TO_CHAR` é a função válida para formatar números como strings no Oracle e outros bancos SQL

 Formato monetário adequado:
- `'$999990.99'` é um formato que:
- Mostra o símbolo de dólar (`$`)
- Permite até 5 dígitos antes do ponto (`99999`)
-  Mostra sempre 2 casas decimais (`.99`)
- Inclui um `0` extra para garantir que o número `0` seja mostrado como `$0.00` (ao invés de apenas `$.00`)
---

# Joins 

**Uso da Cláusula ON para estabelecer a condição de Junção**

A condição da junção natural é basicamente uma equijunção de todas as campos com o mesmo nome. Para especificar condições arbitrárias ou campos a serem unidas, é usada a cláusula ON. A condição de junção é separada de outras condições de pesquisa. A cláusula ON facilita a compreensão do código.

## **1. Conceito Fundamental: Por que precisamos de junções?**

Quando dados estão distribuídos em várias tabelas (normalização), usamos **junções** para combiná-los de forma lógica.

**Exemplo Prático:**

- Tabela `EMP` (funcionários): contém `EMPNO`, `ENAME`, `DEPTNO`

- Tabela `DEPT` (departamentos): contém `DEPTNO`, `DNAME`, `LOC`


Precisamos mostrar o nome do funcionário **junto com** seu departamento e localização.

---
#### **2. Como Funciona uma Junção? (Passo a Passo)**

Imagine as tabelas assim:

**Tabela EMP:**

|EMPNO|ENAME|DEPTNO|
|---|---|---|
|7369|SMITH|20|
|7499|ALLEN|30|
|7521|WARD|30|

**Tabela DEPT:**

|DEPTNO|DNAME|LOC|
|---|---|---|
|10|ACCOUNTING|NEW YORK|
|20|RESEARCH|DALLAS|
|30|SALES|CHICAGO|

### **Processo de Junção:**

1. O SQL pega o primeiro registro da tabela `EMP` (SMITH, DEPTNO=20)
2. Procura em `DEPT` onde `DEPTNO=20`
3. Encontra "RESEARCH, DALLAS"
4. Combina os dados:
==SMITH (do EMP) + RESEARCH/DALLAS (do DEPT)==
5. Repete para todos os registros.

#### **3. Tipos de Junções**

 ## a)**INNER JOIN (Junção Interna)**

**O que faz?**  
Retorna **apenas** os registros que têm correspondência em AMBAS as tabelas.

**Sintaxe:**
```SQL
SELECT colunas
FROM tabela1
INNER JOIN tabela2 ON tabela1.chave = tabela2.chave
```

**Exemplo:**
```SQL
SELECT E.ENAME, D.DNAME, D.LOC
FROM EMP E
INNER JOIN DEPT D ON E.DEPTNO = D.DEPTNO;
```

**Resultado:**

| ENAME | DNAME    | LOC     |
| ----- | -------- | ------- |
| SMITH | RESEARCH | DALLAS  |
| ALLEN | SALES    | CHICAGO |
| WARD  | SALES    | CHICAGO |

Se um funcionário tiver `DEPTNULL` ou um `DEPTNO` que não existe em `DEPT`, ele **não aparecerá** no resultado.

-----

 **b) LEFT JOIN (Junção à Esquerda)**

**O que faz?**  
Retorna **TODOS** os registros da tabela à esquerda (`EMP`), mesmo sem correspondência em `DEPT`.

**Exemplo:**
```SQL
SELECT E.ENAME, D.DNAME
FROM EMP E
LEFT JOIN DEPT D ON E.DEPTNO = D.DEPTNO;
```

**Se existir um funcionário sem departamento:**

| ENAME | DNAME    |                                |
| ----- | -------- | ------------------------------ |
| SMITH | RESEARCH |                                |
| ALLEN | SALES    |                                |
| WARD  | SALES    |                                |
| JONES | NULL     | ← Funcionário sem departamento |

---

 **c) RIGHT JOIN (Junção à Direita)**

**O que faz?**  
Retorna **TODOS** os registros da tabela à direita (`DEPT`), mesmo sem funcionários.

**Exemplo:**
```SQL
SELECT E.ENAME, D.DNAME
FROM EMP E
RIGHT JOIN DEPT D ON E.DEPTNO = D.DEPTNO;
```

**Se existir um departamento sem funcionários:**

|ENAME|DNAME|
|---|---|
|SMITH|RESEARCH|
|ALLEN|SALES|
|WARD|SALES|
|NULL|ACCOUNTING|← Departamento sem funcionários|

---

 **d) FULL JOIN (Junção Completa)**

**O que faz?**  
Retorna **TODOS** os registros de ambas as tabelas, combinando onde possível.

**Exemplo:**
```SQL
SELECT E.ENAME, D.DNAME
FROM EMP E
FULL JOIN DEPT D ON E.DEPTNO = D.DEPTNO;
```

**Resultado hipotético:**

| ENAME | DNAME      |                                 |
| ----- | ---------- | ------------------------------- |
| SMITH | RESEARCH   |                                 |
| ALLEN | SALES      |                                 |
| WARD  | SALES      |                                 |
| JONES | NULL       | ← Funcionário sem departamento  |
| NULL  | ACCOUNTING | ← Departamento sem funcionários |

---

 **4. Autojunção (SELF JOIN)**

**Quando usar?**  
Quando uma tabela referencia a si mesma (ex.: tabela de funcionários onde cada um tem um gerente).

**Estrutura da Tabela:**

| EMPNO | ENAME | MGR  |                              |
| ----- | ----- | ---- | ---------------------------- |
| 7369  | SMITH | 7902 |                              |
| 7499  | ALLEN | 7698 |                              |
| 7902  | FORD  | NULL | ← Presidente não tem gerente |

**Consulta:**
```SQL
SELECT F.ENAME AS FUNCIONARIO, G.ENAME AS GERENTE
FROM EMP F
LEFT JOIN EMP G ON F.MGR = G.EMPNO;
```

**Resultado:**

| FUNCIONARIO | GERENTE |                   |
| ----------- | ------- | ----------------- |
| SMITH       | FORD    |                   |
| ALLEN       | BLAKE   |                   |
| FORD        | NULL    | ← Não tem gerente |

 **5. Erros Comuns e Como Evitá-los**

### **Problema 1: Coluna Ambígua**

**Mensagem:**  
`ORA-00918: column ambiguously defined`

**Causa:**  
Duas tabelas têm colunas com o mesmo nome (ex.: `DEPTNO` em `EMP` e `DEPT`).

**Solução:**  
Sempre prefixe com o nome/apelido da tabela:
```SQl
-- ERRADO (ambíguo)
SELECT DEPTNO FROM EMP JOIN DEPT ON... 

-- CORRETO
SELECT EMP.DEPTNO, DEPT.DNAME 
FROM EMP JOIN DEPT ON EMP.DEPTNO = DEPT.DEPTNO;
```

 **Problema 2: Junção Incorreta**

**Causa:**  
Usar `WHERE` em vez de `ON` para junções.

**Solução:**
```SQL
-- ERRADO (filtra após a junção)
SELECT * FROM EMP, DEPT WHERE EMP.DEPTNO = DEPT.DEPTNO;

-- CORRETO (junção explícita)
SELECT * FROM EMP INNER JOIN DEPT ON EMP.DEPTNO = DEPT.DEPTNO;
```

## **Resumo Visual das Junções**

| Tipo de Junção | Retorna                                 | Sintaxe SQL                       |
| -------------- | --------------------------------------- | --------------------------------- |
| **INNER JOIN** | Apenas correspondências                 | `FROM A INNER JOIN B ON A.x=B.y`  |
| **LEFT JOIN**  | Tudo de A + correspondências em B       | `FROM A LEFT JOIN B ON A.x=B.y`   |
| **RIGHT JOIN** | Tudo de B + correspondências em A       | `FROM A RIGHT JOIN B ON A.x=B.y`  |
| **FULL JOIN**  | Tudo de ambas, combinando onde possível | `FROM A FULL JOIN B ON A.x=B.y`   |
| **SELF JOIN**  | Junção da tabela com ela mesma          | `FROM A X JOIN A Y ON X.pai=Y.id` |

**Junções Externas – OuterJoin**

Caso um registro não satisfizer uma condição de junção, o registro não aparecere no relatório da consulta. Por exemplo, na equijoin das tabelas EMP e DEPT, o departamento 40 OPERATIONS não aparece porque nenhum empregado trabalha neste departamento. Os registros ausentes, podem ser regastados, caso um operador de _outerjoin_ seja usado na condição de junção.

![[Pasted image 20250324165451.png]]

O Outer Join é um tipo de junção em SQL que permite incluir no resultado **todos os registros de uma tabela**, mesmo quando não há correspondência na outra tabela. É extremamente útil quando você precisa:

- Manter todos os registros de uma tabela principal
    
- Incluir informações relacionadas quando existirem
    
- Identificar registros "órfãos" (sem relacionamento)

## **Quando Usar Cada Tipo?**

|Tipo|Quando Usar|Exemplo Comum|
|---|---|---|
|**LEFT JOIN**|Quando você quer todos os registros da tabela principal, mesmo sem relação|Todos os clientes, com ou sem pedidos|
|**RIGHT JOIN**|Quando você quer todos os registros da tabela secundária, mesmo sem relação|Todos os produtos, mesmo não vendidos|
|**FULL JOIN**|Quando precisa de todos os registros de ambas tabelas|Relatório completo de relacionamentos|

## **Diferença Crucial: Outer Join vs Inner Join**
```SQL
-- Inner Join (apenas correspondências)
SELECT E.ename, D.dname
FROM emp E
INNER JOIN dept D ON E.deptno = D.deptno;

-- Left Outer Join (todos os empregados)
SELECT E.ename, D.dname
FROM emp E
LEFT JOIN dept D ON E.deptno = D.deptno;
```

```SQL
-- INNER JOIN
ENAME   DNAME
------  --------
SMITH   RESEARCH
ALLEN   SALES
WARD    SALES

-- LEFT JOIN
ENAME   DNAME
------  --------
SMITH   RESEARCH
ALLEN   SALES
WARD    SALES
JONES   NULL     ← Aparece no LEFT mas não no INNER
```

# Auto Join em SQL:
O Auto Join (ou "Self Join") é uma técnica poderosa em SQL que permite **juntar uma tabela a si mesma**. É especialmente útil quando você precisa:

- Analisar relações hierárquicas (como gerentes-subordinados)
- Comparar registros dentro da mesma tabela
- Encontrar relacionamentos entre entidades do mesmo tipo

## **Como Funciona o Auto Join?**

Imagine uma tabela de funcionários onde cada registro sabe quem é seu gerente:

### **Estrutura da Tabela EMP**

|EMPNO|ENAME|JOB|MGR|DEPTNO|
|---|---|---|---|---|
|7839|KING|PRESIDENT|NULL|10|
|7698|BLAKE|MANAGER|7839|30|
|7782|CLARK|MANAGER|7839|10|
|7566|JONES|MANAGER|7839|20|
|7499|ALLEN|SALESMAN|7698|30|

Note que:

- `MGR` (Manager) é o `EMPNO` do gerente
- KING não tem gerente (`MGR` é NULL)

```SQL
SELECT a.coluna1, b.coluna2
FROM tabela a
JOIN tabela b ON a.chave = b.chave_relacionada
```

## **Exemplo Prático 1: Hierarquia de Gerência**

```SQL
SELECT 
   e.ename AS funcionario,
   m.ename AS gerente
FROM 
   emp e
LEFT JOIN 
   emp m ON e.mgr = m.empno;
```

**Resultado:**

|FUNCIONARIO|GERENTE|
|---|---|
|BLAKE|KING|
|CLARK|KING|
|JONES|KING|
|ALLEN|BLAKE|
|KING|NULL|

👉 **Observe que**:

- Usamos `LEFT JOIN` para incluir KING (que não tem gerente)
    
- A tabela `emp` é referenciada duas vezes com aliases diferentes (`e` e `m`)
    

## **Exemplo Prático 2: Encontrar Colegas de Departamento**

```SQL
SELECT 
   a.ename AS funcionario1,
   b.ename AS funcionario2,
   a.deptno
FROM 
   emp a
JOIN 
   emp b ON a.deptno = b.deptno AND a.empno < b.empno;
```

**Resultado:**

|FUNCIONARIO1|FUNCIONARIO2|DEPTNO|
|---|---|---|
|BLAKE|ALLEN|30|
|CLARK|KING|10|

👉 **Por que `a.empno < b.empno`?**  
Evita duplicatas (ex: "BLAKE-ALLEN" e "ALLEN-BLAKE")

#### **Casos de Uso Comuns**

1. **Estruturas Hierárquicas**:

- Organogramas empresariais

- Estruturas de pastas em sistemas de arquivos
   
2. **Relacionamentos Recursivos**:

- Amizades em redes sociais

- Componentes que usam outros componentes

3. **Análise Comparativa**:

- Comparar vendas entre vendedores da mesma região

- Identificar produtos similares

#### **Diferença Entre Auto Join e Junções Tradicionais**

|Característica|Auto Join|Junção Tradicional|
|---|---|---|
|Tabelas envolvidas|Mesma tabela (2 alias)|Tabelas diferentes|
|Propósito principal|Analisar relações internas|Relacionar dados distintos|
|Complexidade|Maior cuidado com alias|Mais intuitiva|

## **Dicas de Performance**

1. **Use índices** nas colunas de junção
2. **Filtre cedo** com WHERE quando possível
3. **Evite SELECT *** - liste apenas as colunas necessárias

-----
## Funções de Grupo e Subconsultas

Uma subconsulta é uma  consulta utilizada dentro de uma instrução SQL. Pode ser utilizada dentro de instruções select, insert, delete update ou create table.

### **Funções de Grupo em SQL**

As funções de grupo operam em conjuntos de linhas para fornecer um resultado por grupo. Essas operações podem envolver:

- Todas as linhas de uma tabela, ou
    
- Conjuntos de linhas definidos por critérios pré-estabelecidos.
    

Assim como em outras linguagens ou aplicativos, as funções SQL requerem argumentos (representados pelo nome da coluna) e retornam valores. A sintaxe básica é:

```SQL
FUNÇÃO(coluna)
```

---

### **Funções Disponíveis**

|Função|Descrição|
|---|---|
|`AVG()`|Retorna a média dos valores de um conjunto.|
|`COUNT()`|Retorna a quantidade de ocorrências.|
|`MAX()`|Retorna o maior valor de um conjunto.|
|`MIN()`|Retorna o menor valor de um conjunto.|
|`SUM()`|Retorna a somatória dos valores.|
|`VARIANCE()`|Retorna a variância entre os valores.|

---
**Sintaxe Completa**

```SQL
SELECT [coluna,] função_de_grupo(coluna)
FROM tabela
[WHERE condição]
[GROUP BY coluna]
[HAVING condição]
[ORDER BY coluna];
```
#### **Explicação das Cláusulas**

- **`[coluna,]`**: Lista opcional de colunas envolvidas na consulta.
    
- **`função_de_grupo(coluna)`**: Função aplicada aos dados da coluna especificada.
    
- **`FROM tabela`**: Tabela(s) consultada(s).
    
- **`WHERE condição`**: Filtra linhas antes do agrupamento.
    
- **`GROUP BY coluna`**: Agrupa os dados pela coluna especificada.
    
- **`HAVING condição`**: Filtra grupos (similar ao `WHERE`, mas para colunas agrupadas).
    
- **`ORDER BY coluna`**: Ordena os resultados (ascendente por padrão).

---
### **Observações Importantes**

1. **Valores Nulos**:
    
    - Todas as funções de grupo (exceto `COUNT(*)`) ignoram valores nulos.
  
#### Linguagem SQL e Comandos DDL

É através da linguagem SQL que interagimos com o SGBD. Essa linguagem é composta de categorias de comandos. São elas DDL (comandos de definição de estruturas), DML (comandos de manipulação de dados, DCL (comandos de controle) e DQL (comandos de consulta).

Conhecer os comandos da linguagem SQL é fundamental para acessar o SGBD, manipular estruturas de armazenamento e seus dados.

**DDL – Data Definition Language – Trabalhando Com Tabelas**

A DDL é a parte da SQL usada para criar e manipular objetos que se relacionam aos dados, especialmente tabelas. Com a DDL você pode criar uma tabela, configurar suas colunas e todas as restrições de integridade, por isso antes de começarmos a escrever nossos primeiros comandos temos que entender bem a linguagem SQL e as restrições de integridade envolvidas.

A DDL está intimamente ligada também a modelagem física do banco de dados, pois é nessa parte do projeto onde os modelos lógicos são derivados para um banco de dados real, ou seja, se tornam físicos (saem do papel).

Vamos começar entendendo a sintaxe do comando que é capaz de criar uma tabela, o CREATE TABLE, que funciona da seguinte forma:

![[Pasted image 20250311090907.png]]

Para entender melhor este comando, vamos utilizá-lo em um modelo real. A modelagem conceitual pode ser vista na figura 1, onde estamos criando a base de dados de um pequeno jogo, onde cada personagem é de um tipo e possui um ou mais poderes (somente esta parte do jogo). A figura 2 mostra a derivação do respectivo contexto para a modelagem lógica.

![[Pasted image 20250311092519.png]]

Vamos começar a implementação física deste cenário pela tabela mais simples, ou seja, a que possui menos restrições e não depende de nenhuma outra tabela para existir. Neste caso temos as tabelas “tipo” e “poder”. A tabela “personagem”, por exemplo, possui uma chave estrangeira para “tipo” e, por isso, não poderíamos começar por ela, a não ser que façamos a inclusão da restrição referencial depois, alterando-a.

![[Pasted image 20250311092936.png]]

Repare que assim como na modelagem lógica, a restrição da chave primária recebe um nome, nesse caso “tipo_pk”. Isso ocorre nas restrições de chave e referencial. Ao se incluir a restrição de chave é necessário informar qual é a coluna que recebe essa restrição, neste caso a coluna “idTipo”. Seguindo a mesma lógica, criamos as próximas tabelas.

![[Pasted image 20250311093114.png]]

![[Pasted image 20250311093135.png]]

Repare na criação da tabela “personagem” que há a restrição referencial sendo aplicada com o acréscimo da CONSTRAINT do tipo FOREIGN KEY. Lembre-se que toda restrição, no Oracle, deve ter um nome e, no caso da chave estrangeira, é preciso informar qual coluna local a recebe e qual o “alvo”, ou seja, a tabela e sua respectiva coluna de chave primária.

Por fim, vamos criar a tabela de relacionamento entre “personagem” e “poder”, pois como a relação é N:N (cada personagem pode possuir N poderes e cada poder pode estar associado a N personagens), temos que as relacionar através de uma terceira tabela, conforme:

![[Pasted image 20250311093321.png]]

Repare nas quebras de linhas e a indentação (afastamento da margem) são diferentes para cada comando. Isso quer dizer que não importa se as linhas estão quebradas ou não para a execução do script, mas aqui são descritas assim para maior legibilidade. Essa é, inclusive, uma forte recomendação da comunidade internacional e de qualquer manual de bancos de dados. Repare, ainda, que todos os comandos foram escritos com letras maiúsculas e isso também poderia ter sido diferente, ou seja cada comando poderia ter sido escrito completamente em letras minúsculas, mas por boas práticas de programação escrevemos as palavras reservadas da SQL em letras maiúsculas e o nome dos objetos criados por nós mesmos em letras minúsculas. Por fim, e não menos importante, repare que ao final de cada comando há um “;” que especifica sua finalização.

Se você precisar excluir uma tabela, deve-se utilizar o comando “DROP TABLE nome_da_tabela;”, por exemplo “DROP TABLE tipo;” e a tabela tipo será eliminada do banco de dados. Deve-se utilizar este comando com muito cuidado.

Para se alterar dados de uma tabela, utiliza-se o comando “ALTER TABLE nome_da_tabela MODIFY (modificações);”. A palavra reservada “MODIFY” pode ser substituída por “ADD” se você está adicionando algo na tabela. Por exemplo, se você precisa alterar que a altura do personagem não pode ser nula, deve-se executar o comando “ALTER TABLE personagem MODIFY (altura NOT NULL);” e se você precisar acrescentar uma nova coluna chamada “idade” (que refere-se à idade da personagem), o comando “ALTER TABLE personagem ADD idade NUMBER(2) NULL;” deve ser executado.

Na criação de tabelas, usa-se um comando  DDL. Para criar uma tabela é necessário que o usuário tenha privilégio e uma área para armazenamento. A sintaxe simplificada para criação de tabelas é:


`**Sintaxe: CREATE TABLE** [_esquema._]_tabela_`
          `(nome da coluna _tipo do  dado_ [DEFAULT _expr_]`
              `_[constraint da coluna],_`
              `_...,_`
              `_[constraint da tabela]);_`

onde:

|   |   |
|---|---|
|_Esquema:_|é o  nome do proprietário da tabela, quando omitido a tabela é criada no esquema do usuário corrente|
|_Tabela:_|é o nome da tabela|
|_DEFAULT expr:_|especifica um valor default que será utilizado quando um dado for omitido na inserção|
|_Coluna:_|é o nome da coluna|
|_tipo de dados:_|é o tipo de dados e o comprimento da coluna|
|_Constraint:_|Está cláusula é opcional e especifica as restrições para a coluna ou para a tabela, quando o nome da constraint é omitido o Oracle assume uma identificação|

Convenções para Nomeação de Tabelas e Colunas:

• Deve começar com uma letra

• Pode ter de 1 a 30 caracteres (depende do SGBD)

• Deve conter somente A–Z, a–z, 0–9, _, $ e #

• Não deve duplicar o nome de outro objeto de propriedade do mesmo usuário

• Não deve ser uma palavra reservada pelo Oracle Server

Tipos de Dados:

![[Pasted image 20250311093856.png]]


No exemplo abaixo está sendo criada  a tabela DEPT, com três colunas — chamadas, DEPTNO, DNAME e LOC.

SQL>CREATE TABLE dept  
  2      (deptno NUMBER(2),

  3      dname          VARCHAR2(14),

  4      loc      VARCHAR2(13));

Table created.

A instrução Describe é utilizada para exibir a estrutura de uma tabela.

SQL> DESCRIBE dept

Name                Null?    Type

------------------ -------- ---------

DEPTNO                      NUMBER(2)

DNAME                       VARCHAR2(14)

LOC                         VARCHAR2(13)

---
**Restrições de Integridade**

São elas chaves primárias, chaves estrangeiras, colunas de dados únicos, não nulos etc., especialmente na modelagem lógica. Quando uma restrição é “violada” (não é atendida) é muito mais fácil encontrarmos a origem do erro. Os bancos de dados chamam as restrições com seu termo em inglês, ou seja, “CONSTRAINT”.

As restrições de integridade servem para impedir que dados inválidos sejam inseridos numa determinada coluna e são garantidas pelo próprio SGBD (Sistema Gerenciador de Banco de Dados), nós apenas as configuramos na hora de criar os objetos (através da DDL). Podemos, inclusive, dizer que as restrições (CONSTRAINTS) impõem regras nas colunas. Essas restrições são divididas em seis grupos, sendo:

- Restrição de integridade de **domínio**
- Restrição de integridade de **chave**
- Restrição de integridade **nula**
- Restrição de integridade **referencial**
- Restrição de integridade **unicidade**
- Restrição de integridade **de valor padrão**

A integridade de domínio especifica qual **tipo de valor** um determinado atributo pode admitir, ou seja, é são os tipos de dados (datatypes). Por exemplo, colunas configuradas como número inteiro, número de ponto flutuante, texto, data com hora, somente data, etc. Se um dado do tipo texto for inserido em uma coluna que aceita apenas valores numéricos, a restrição de integridade de domínio será violada. A integridade de domínio pode ir além, podendo **checar** se um valor inserido está dentro de uma especificação. Para isso, utiliza-se a restrição “CHECK”. Por exemplo, o estado no cadastro de um endereço, deve ser uma das 27 opções; o sexo de uma pessoa etc.

A integridade de vazio especifica se o valor de um atributo **pode ou não ser vazio**, ou seja, nulo. São os famosos NULL (permite que um dado seja vazio) e NOT NULL (não permite que um dado não seja especificado naquela coluna na hora de inserir uma linha). A integridade de vazio é também associada à cardinalidade mínima nos relacionamentos (0, a FK pode ser nula. 1, a FK não pode ser nula).

Já a integridade de chave (ou como alguns autores chamam, integridade de chave primária) garante que os valores das chaves primárias sejam sempre únicos e não nulos, pela própria definição de chave primária. Por exemplo, se tentarmos inserir uma linha cuja chave primária já exista, haverá violação da restrição de chave primária.

A integridade referencial é a integridade das FKs (chaves estrangeiras – _Foreign Keys_). Ela garante que o valor que aparecer nos atributos de uma chave estrangeira deve sempre aparecer na chave primária da tabela referenciada, ou seja, garante que todo valor de uma FK seja o mesmo de uma PK, a qual a coluna em questão aponta. Assim sendo, sempre que uma coluna é definida como FK, o SGBD deve garantir que ela sempre aponte para uma PK. Na hora que estamos criando as colunas FKs devemos dizer qual é a tabela alvo e sua respectiva chave primária.

A integridade de unicidade é aquela restrição que permite, ou não, que o valor se repita. No banco de dados utilizamos a palavra reservada UNIQUE quando queremos que seus dados sejam únicos, como por exemplo, o RG de uma pessoa, o e-mail de um usuário, os dados de uma impressão digital etc. Não confunda a restrição de unicidade com a de chave primária, pois os valores dessa coluna não são necessariamente identificadores da tabela.

Por fim e não menos importante temos a integridade de valor padrão associada à palavra reservada DEFAULT. Essa restrição permite que se um valor nulo for inserido em uma coluna (ou não foi informado, por exemplo) um valor padrão (pré-definido) é colocado em seu lugar. Por exemplo, se o país não foi informado numa tabela de endereços incluir “Brasil”. Essa restrição está fortemente ligada à restrição de nulo.

É muito importante reforçar que todas as restrições de integridade são garantidas pelo próprio SGBD. Uma restrição que não se encaixa em nenhuma das citadas aqui é chamada de restrição semântica e deve ser garantida pelo software que utiliza o banco de dados. Por exemplo, a cardinalidade máxima de um relacionamento ou, ainda como exemplo real, imagine que temos um relacionamento entre funcionários e departamento, onde um funcionário de recursos humanos não poderia assumir o cargo de analista de sistemas. Essa é uma restrição que deve ser garantida pela própria aplicação.

Pockt Guide

![[Pasted image 20250311095133.png]]

![[Pasted image 20250311095202.png]]

----

# Comandos DML  e DQL

**Introdução** 

É através da linguagem SQL que interagimos com o SGBD. Essa linguagem é composta de categorias de comandos. São elas DDL (comandos de definição de estruturas), DML (comandos de manipulação de dados, DCL (comandos de controle) e DQL (comandos de consulta).

Conhecer os comandos da linguagem SQL é fundamental para acessar o SGBD, manipular estruturas de armazenamento e seus dados.

**Comandos DML**

Os comandos da categoria DML (Data Manipulation Language), servem para realizar  adições, eliminações e atualizações em dados de um ou mais registros de uma ou mais tabelas de maneira concorrente. Os comandos da categoria DML são:

- Insert – Adição de linhas com  dados na tabela
- Update – Atualização de  dados na tabela
- Delete – Eliminação de dados da tabela
- Commit – Confirmação das transações, ou seja, salvamento dos dados
- Rollback – Desistência das transações, ou seja, desfazer a última transação

**A adição de linhas com dados é um comando DML.**

**Sintaxe:**

**INSERT INTO** _tabela_ [(_coluna_ [_, coluna..._])] **VALUES** _(valor_ [_, valor..._])_;_

Onde:

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1693227350131-XB2TF5sprq.png)


### **Verificando a estrutura de uma tabela**

Para visualizar a ordem padrão das colunas e os tipos de dados esperados, utilize o comando `DESCRIBE`:

```
SQL> DESCRIBE dept;
```

📌 **Saída do comando:**

|Nome da Coluna|Permite Nulo?|Tipo de Dado|
|---|---|---|
|**DEPTNO**|NOT NULL|NUMBER(2)|
|**DNAME**|NULL|VARCHAR2(14)|
|**LOC**|NULL|VARCHAR2(13)|

🔹 O comando `DESCRIBE` exibe:

- A **ordem das colunas** na tabela.
- Se a coluna aceita valores **NULL**.
- O **tipo de dado** definido para cada campo.

💡 **Dica:** Sempre use `DESCRIBE` antes de inserir dados para garantir que os valores inseridos correspondam ao tipo esperado.


**Exemplo 1: Inserção completa com colunas especificadas**

```
SQL> INSERT INTO dept (DEPTNO, DNAME, LOC)  
  2  VALUES (80, 'COMERCIAL', 'SP');
```

🔹 Neste exemplo, estamos inserindo um novo departamento (**DEPTNO 80**) chamado **"COMERCIAL"**, localizado em **"SP"**.


**Exemplo 2: Inserção sem especificar colunas (assumindo a ordem da tabela)**

```
SQL> INSERT INTO dept  
  2  VALUES (90, 'FINANCEIRO', 'RJ');
```

🔹 Aqui, os valores estão sendo inseridos diretamente, assumindo que a tabela **`dept`** possui exatamente três colunas na ordem correta (**DEPTNO, DNAME e LOC**).

📌 **Recomendação:** Sempre que possível, especifique os nomes das colunas para evitar problemas caso a estrutura da tabela mude no futuro.

### **Inserção de Dados em Tabelas**


**Exemplo 3: Inserção parcial de dados**

```
SQL> INSERT INTO dept (deptno, dname)  
  2  VALUES (55, 'RH');
```

🔹 A tabela **`dept`** contém as colunas **`deptno`**, **`dname`** e **`loc`**.  
🔹 Como o campo **`loc`** não foi especificado, ele será preenchido automaticamente com **NULL**.


**Exemplo 4: Inserção com valor NULL explícito**

```
SQL> INSERT INTO dept  
  2  VALUES (45, 'DIRETORIA', NULL);
```

🔹 Aqui, os valores estão sendo inseridos diretamente, e o campo **`loc`** recebe **NULL** explicitamente.  
🔹 Isso é útil quando queremos deixar claro que o campo não terá um valor atribuído.


## **Inserção de Dados com Datas**

 **Exemplo 5: Inserindo um registro na tabela `emp`**

```
SQL> INSERT INTO emp  
  2  VALUES (3000, 'JOSE', 'VENDEDOR', 7782, TO_DATE('30/03/23', 'DD/MM/YY'),  
  3          2800, NULL, 20);
```

🔹 **Explicação dos valores inseridos:**

- `3000` → Código do empregado.
- `'JOSE'` → Nome do empregado.
- `'VENDEDOR'` → Cargo.
- `7782` → Código do gerente.
- `TO_DATE('30/03/23', 'DD/MM/YY')` → Data de admissão (convertida para formato de data).
- `2800` → Salário.
- `NULL` → Comissão (não aplicável).
- `20` → Código do departamento.

### **Visualizando os dados inseridos:**

Para verificar os registros na tabela **`emp`**, use:

```
SQL> SELECT *  
  2  FROM emp;
```

## **Atualização de Dados nos Registros**

**Sintaxe do comando `UPDATE`**

```
UPDATE tabela  
SET coluna = valor [, coluna = valor, ...]  
[WHERE condição];  
```

🔹 **Importante:** Se a cláusula `WHERE` for omitida, **todas as linhas** da tabela serão alteradas!

### **Exemplo: Atualizando um registro específico**

Atualizar o departamento para **30** do empregado com código **7900**:

```
SQL> UPDATE emp  
  2  SET deptno = 30  
  3  WHERE empno = 7900;
```

📌 **Sempre utilize a cláusula `WHERE` ao atualizar registros para evitar modificar toda a tabela por engano.**

### **Comando `SELECT`**

O comando `SELECT` é utilizado para realizar consultas aos dados armazenados em uma tabela.

**Exemplo de `SELECT` exibindo todos os dados da tabela `emp`**

```
SQL> SELECT *  
  2  FROM emp;
```

🔹 O asterisco (`*`) indica que **todas as colunas** da tabela serão retornadas na consulta.

## **Sintaxe do Comando `SELECT`**

🔹 **Regras para uso dos comandos SQL:**

- O SQL **não diferencia maiúsculas e minúsculas** no processamento dos comandos.
- Os comandos podem ser escritos em **uma ou mais linhas**.
- **Não é permitido abreviar** as palavras-chave dos comandos.
- **Escrever cada parte do comando em uma linha separada** melhora a legibilidade.
- Para exibir **apenas colunas específicas**, devemos nomeá-las na consulta.

 **Exemplo: Exibir apenas algumas colunas**
```
SQL> SELECT deptno, dname  
  2  FROM dept;
```

🔹 Aqui, estamos consultando apenas as colunas **`deptno`** (número do departamento) e **`dname`** (nome do departamento).

# **Operadores Aritméticos**

Os operadores aritméticos podem ser utilizados em qualquer cláusula de uma instrução SQL, **exceto na cláusula `FROM`**.

![[Pasted image 20250315082302.png]]

 **Exemplo: Exibir o salário original e o salário acrescido de R$ 300,00**

``` SQL
SQL> SELECT ename, sal, sal + 300  
  2  FROM emp;
```

![[Pasted image 20250315082338.png]]
➡️ **Nova coluna gerada apenas para exibição:** O resultado apresentará os nomes dos empregados (**`ename`**), seus salários originais (**`sal`**) e uma **coluna extra** mostrando os salários com um acréscimo de R$ 300,00.

### **Ordem de precedência matemática**

As regras matemáticas e a ordem de precedência continuam válidas dentro do SQL.

``` SQL
 SQL> SELECT ename, sal, sal + ((sal * 30) / 100)  
  2  FROM emp;
```

➡️ Aqui, estamos calculando o salário acrescido de **30%**.

✅ **Dica:** Use **parênteses** para garantir a ordem correta dos cálculos.

# **Operadores de Comparação**

Os operadores de comparação são utilizados para **estabelecer relações entre valores ou expressões**.

- O resultado de uma comparação é sempre um valor **booleano** (`TRUE` ou `FALSE`).
- Podem ser usados em **comparações que envolvem apenas uma linha**.

![[Pasted image 20250315082444.png]]

### **Operador `BETWEEN`**

Os valores especificados com `BETWEEN` são **inclusivos**. O limite **inferior** deve ser especificado primeiro.

```SQL
SQL> SELECT ename, sal  
  2  FROM emp  
  3  WHERE sal BETWEEN 1000 AND 1500;
```

➡️ Retorna os funcionários cujo salário está **entre R$ 1.000 e R$ 1.500** (inclusive).

### **Operador `IN`**

Verifica se um valor está presente em uma **lista de valores específicos**.

```SQL
SQL> SELECT empno, ename, mgr, deptno  
  2  FROM emp  
  3  WHERE ename IN ('FORD', 'ALLEN');
```

➡️ Retorna os funcionários cujo nome seja **"FORD"** ou **"ALLEN"**.

✅ Se forem utilizados **caracteres ou datas**, eles devem estar entre **aspas simples (`'`)**:

```SQL
SQL> SELECT empno, ename, mgr, deptno  
  2  FROM scott.emp  
  3  WHERE job IN ('PRESIDENT', 'MANAGER');
```

➡️ Retorna funcionários cujo cargo (`job`) seja **"PRESIDENT"** ou **"MANAGER"**.

### **Operador `LIKE`**

O operador `LIKE` permite buscar registros que **correspondam a um padrão de caracteres**.

```SQL 
SQL> SELECT ename  
  2  FROM scott.emp  
  3  WHERE ename LIKE 'J%';
```

➡️ Retorna todos os funcionários cujo nome começa com **"J"** (letra maiúscula).  
🔹 Se houver nomes iniciados com **"j" minúsculo**, eles **não serão retornados**.

✅ **Símbolos utilizados no `LIKE`**:

- `%` → Representa **qualquer sequência de caracteres**.
    - Exemplo: `'A%'` encontra **"Ana"**, **"Antonio"**, **"Alberto"**, etc.
- `_` → Representa **um único caractere**.
    - Exemplo: `'A_'` encontra **"Ao"**, **"An"**, mas não **"Ana"**.

---

### **Operador `IS NULL`**

Usado para verificar campos que **não possuem valor** (`NULL`).

```SQL
SQL> SELECT ename, job, deptno  
  2  FROM scott.emp  
  3  WHERE comm IS NULL;
```

➡️ Retorna os funcionários que **não recebem comissão** (`comm` está `NULL`).

✅ **Importante:** `NULL` significa **ausência de valor**.  
❌ **Não podemos usar `=` ou `!=` para comparar valores `NULL`**, pois `NULL` **não é igual nem diferente de nada**.

# **Operadores Lógicos**

Os operadores lógicos permitem combinar múltiplas condições para gerar um **único resultado**.  
✅ **Principais operadores lógicos no SQL:**

1. **`AND`** → Ambas as condições devem ser **verdadeiras**.
2. **`OR`** → Pelo menos **uma** das condições deve ser verdadeira.
3. **`NOT`** → Inverte o resultado da condição.

 **Exemplo: Filtrar funcionários com salário maior que 2000 e que pertencem ao departamento 30**

```SQL
SQL> SELECT ename, sal, deptno  
  2  FROM emp  
  3  WHERE sal > 2000 AND deptno = 30;
```

➡️ Apenas os funcionários do **departamento 30** com **salário superior a R$ 2.000** serão retornados.

# **Operadores Lógicos no SQL**

Os operadores lógicos são utilizados para **combinar expressões** na cláusula `WHERE`. Eles podem ser aplicados em **consultas (`SELECT`)**, **atualizações (`UPDATE`)** e **exclusões (`DELETE`)** de dados.

## **Operador `AND`**

O operador `AND` retorna resultados **apenas quando todas as condições são verdadeiras**.

**Exemplo: Selecionar funcionários com salário ≥ 1100 e cargo `SALESMAN`**

```SQL
SQL> SELECT empno, ename, job, sal  
  2  FROM scott.emp  
  3  WHERE sal >= 1100 AND job = 'SALESMAN';
```

✅ **Resultado:**

``` 
EMPNO     ENAME      JOB        SAL  
7876      ADAMS      SALESMAN   1100  
7934      MILLER     SALESMAN   1300  
```

- Apenas os funcionários que atendem **ambas as condições** (`sal >= 1100` **E** `job = 'SALESMAN'`) são selecionados.
- Se qualquer condição for **falsa**, a linha não será incluída no resultado.

⚠️ **Cuidado com maiúsculas e minúsculas em valores alfanuméricos!**

- SQL **distingue letras maiúsculas e minúsculas**. No exemplo acima, `SALESMAN` deve estar em **maiúsculas**, caso contrário, nenhum resultado será retornado.

## **Operador `OR`**

O operador `OR` retorna resultados **quando pelo menos uma das condições for verdadeira**.

**Exemplo: Selecionar funcionários com salário ≥ 1100 ou cargo `SALESMAN`**

``` SQL
 SELECT empno, ename, job, sal  
  2  FROM emp  
  3  WHERE sal >= 1100 OR job = 'SALESMAN';
```

✅ **Resultado (parcial):**

```
EMPNO     ENAME     JOB         SAL  
7839      KING      PRESIDENT   5000  
7698      BLAKE     MANAGER     2850  
7782      CLARK     MANAGER     2450  
7566      JONES     MANAGER     2975  
7654      MARTIN    SALESMAN    1250  
...
```

- Se um funcionário **tiver salário ≥ 1100** **OU** **for `SALESMAN`**, ele será incluído no resultado.
- Funcionários que atendem **apenas uma das condições** também aparecem na consulta.

## **Operador `NOT`**

O operador `NOT` **inverte o resultado de uma condição**.

### **Exemplo: Selecionar funcionários que NÃO sejam `CLERK`, `MANAGER` ou `ANALYST`**

```
SQL> SELECT ename, job  
  2  FROM scott.emp  
  3  WHERE job NOT IN ('CLERK', 'MANAGER', 'ANALYST');
```

✅ **Resultado:**

```
ENAME      JOB  
KING       PRESIDENT  
MARTIN     SALESMAN  
ALLEN      SALESMAN  
TURNER     SALESMAN  
WARD       SALESMAN  
```

- **Apenas os funcionários que NÃO possuem os cargos listados** (`CLERK`, `MANAGER`, `ANALYST`) aparecem no resultado.

✅ **`NOT` pode ser combinado com outros operadores:**

```
... WHERE job   NOT IN ('SALESMAN', 'MANAGER');  -- Exclui SALESMAN e MANAGER  
... WHERE sal   NOT BETWEEN 2500 AND 5000;      -- Exclui salários entre 2500 e 5000  
... WHERE ename NOT LIKE '%S%';                 -- Exclui nomes que contenham "S"  
... WHERE comm  IS   NOT NULL;                  -- Seleciona funcionários com comissão  
```

# **Controle de Transações (COMMIT & ROLLBACK)**

As transações garantem que um conjunto de operações **DML** (`INSERT`, `UPDATE`, `DELETE`) seja executado corretamente no banco de dados.

### **Requisitos das transações:**

✔ **Consistência** → Os dados devem permanecer íntegros.  
✔ **Atomicidade** → Todas as operações devem ser concluídas com sucesso ou nenhuma será realizada.  
✔ **Integridade** → O banco de dados deve sempre manter um estado válido.

🚀 **Exemplo prático: Transferência de dinheiro**

1. Debita um valor da conta A (`UPDATE` na conta de origem).
2. Credita o mesmo valor na conta B (`UPDATE` na conta de destino).
3. **Se ambos os passos forem bem-sucedidos**, a transação é **confirmada (`COMMIT`)**.
4. **Se houver erro**, a transação é **desfeita (`ROLLBACK`)**.

---

## **COMMIT & ROLLBACK**

📌 **COMMIT** → Confirma as alterações no banco de dados de forma permanente.  
📌 **ROLLBACK** → Desfaz as alterações, retornando o banco ao estado anterior.

### **Eventos que finalizam uma transação:**

✅ **Quando um `COMMIT` ou `ROLLBACK` é emitido explicitamente.**  
✅ **Ao executar um comando DDL (`CREATE`, `ALTER`, `DROP`).**  
✅ **Se o usuário sair do sistema sem confirmar (`COMMIT`) ou cancelar (`ROLLBACK`).**  
✅ **Se houver falha no sistema, ocorre um `ROLLBACK` automático.**

---

**Exemplo: Alterar o departamento de um funcionário e confirmar a transação**

```
SQL> UPDATE emp  
  2  SET deptno = 10  
  3  WHERE empno = 7900;
```

➡️ **Antes do `COMMIT`**, a alteração está apenas na memória.

✅ **Para salvar definitivamente:**

```SQL
COMMIT;
```

✅ **Para desfazer a alteração antes do `COMMIT`:**

```SQL
ROLLBACK;
```

🔹 Se `ROLLBACK` for usado antes do `COMMIT`, **as alterações serão desfeitas**.

![[Pasted image 20250315084422.png]]

**Exemplo do comando rollback:** Excluir todas as linhas da tabela employees

![[Pasted image 20250315084451.png]]

Com o comando Rollback, a alteração provocada é desfeita e a versão original da tabela é restabelecida.

----
👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾
## Consulta com Funções de uma única Linha

É através da linguagem SQL que interagimos com o SGBD. Essa linguagem é composta de categorias de comandos. São elas DDL (comandos de definição de estruturas), DML (comandos de manipulação de dados, DCL (comandos de controle) e DQL (comandos de consulta).

Conhecer os comandos da linguagem SQL é fundamental para acessar o SGBD, manipular estruturas de armazenamento e seus dados.

**Resumo**
É possível realizar operações aritméticas entre os campos de uma tabela dentro do comando Select. Entenda que trata-se apenas de uma consulta, nenhum dado está sendo alterado. Veja o exemplo:

![[Pasted image 20250316074645.png]]

O comando acima calcula o salário anual dos funcionários. Com os Operadores aritméticos podemos realizar expressões aritméticas. Veja o exemplo:

![[Pasted image 20250316074749.png]]

Observe, que nessa consulta, é feito o cálculo do salário anual, o valor do bônus anual que corresponde a 40% do salário anual e o valor total com a soma do salário anual e o bônus.

----

### Consulta com Funções de uma única Linha

É através da linguagem SQL que interagimos com o SGBD. Essa linguagem é composta de categorias de comandos. São elas DDL (comandos de definição de estruturas), DML (comandos de manipulação de dados, DCL (comandos de controle) e DQL (comandos de consulta).

-> Revisando 

É através da linguagem SQL que interagimos com o SGBD. Essa linguagem é composta de categorias de comandos. São elas DDL (comandos de definição de estruturas), DML (comandos de manipulação de dados, DCL (comandos de controle) e DQL (comandos de consulta).
#### 1. DDL (Data Definition Language) - Linguagem de Definição de Dados

Comandos para definir a estrutura do banco de dados (criar, alterar e excluir objetos).

**Exemplos:**
``` SQL
-- Criar uma tabela
CREATE TABLE clientes (
    id INT PRIMARY KEY,
    nome VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    data_cadastro DATE DEFAULT CURRENT_DATE
);

-- Alterar uma tabela (adicionar coluna)
ALTER TABLE clientes ADD COLUMN telefone VARCHAR(20);

-- Excluir uma tabela
DROP TABLE clientes;

-- Criar um índice
CREATE INDEX idx_nome ON clientes(nome);

-- Criar uma view
CREATE VIEW clientes_ativos AS
SELECT * FROM clientes WHERE ativo = TRUE;
```
#### 2. DML (Data Manipulation Language) - Linguagem de Manipulação de Dados

Comandos para manipular os dados armazenados (inserir, atualizar, deletar).

**Exemplos:**

```SQL
-- Inserir dados
INSERT INTO clientes (id, nome, email) 
VALUES (1, 'João Silva', 'joao@email.com');

-- Atualizar dados
UPDATE clientes 
SET telefone = '11999998888' 
WHERE id = 1;

-- Deletar dados
DELETE FROM clientes 
WHERE id = 1;

-- Inserir múltiplos registros
INSERT INTO clientes (id, nome, email) VALUES
(2, 'Maria Souza', 'maria@email.com'),
(3, 'Carlos Lima', 'carlos@email.com');
```

#### 3. DQL (Data Query Language) - Linguagem de Consulta de Dados

Comandos para consultar dados (basicamente o SELECT).

**Exemplos:**

``` SQL
-- Consulta simples
SELECT * FROM clientes;

-- Consulta com filtro
SELECT nome, email FROM clientes 
WHERE data_cadastro > '2023-01-01';

-- Consulta com ordenação
SELECT * FROM clientes 
ORDER BY nome ASC;

-- Consulta com junção de tabelas
SELECT p.descricao, p.preco, c.nome 
FROM produtos p
JOIN clientes c ON p.cliente_id = c.id;

-- Consulta com agregação
SELECT COUNT(*) as total_clientes, 
       AVG(valor_compra) as media_compras
FROM clientes;
```

#### 4. DCL (Data Control Language) - Linguagem de Controle de Dados

Comandos para controlar acesso e permissões.

**Exemplos:**
``` SQL
-- Conceder permissão
GRANT SELECT, INSERT ON clientes TO usuario_app;

-- Revogar permissão
REVOKE DELETE ON clientes FROM usuario_app;

-- Conceder todas as permissões
GRANT ALL PRIVILEGES ON DATABASE meu_banco TO admin;

-- Criar um papel (role) e conceder permissões
CREATE ROLE leitura;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO leitura;
```

## Resumo das categorias:

|Categoria|Propósito|Comandos principais|
|---|---|---|
|DDL|Definir estrutura|CREATE, ALTER, DROP, TRUNCATE, RENAME|
|DML|Manipular dados|INSERT, UPDATE, DELETE, MERGE|
|DQL|Consultar dados|SELECT|
|DCL|Controle de acesso|GRANT, REVOKE, DENY|

Cada tipo de comando tem um propósito específico no gerenciamento e manipulação de bancos de dados relacionais.

### Apelidos (Aliases) em SQL

Os apelidos (ou aliases) em SQL são "apelidos" temporários que você pode atribuir a tabelas ou colunas em suas consultas para tornar o código mais legível ou mais fácil de escrever. Eles são muito úteis em consultas complexas.

### 1. Aliases para Colunas

Usados para renomear colunas nos resultados da consulta.

**Sintaxe:**
```SQL
SELECT 
    nome AS nome_completo,
    email AS endereco_eletronico,
    data_cadastro AS cadastro
FROM clientes;
```

Usados para simplificar referências a tabelas, especialmente em junções.

**Sintaxe:**
```SQL
SELECT 
    c.nome,
    p.descricao
FROM clientes AS c
JOIN pedidos AS p ON c.id = p.cliente_id;
```
1. A palavra-chave `AS` é opcional:
  ```SQL
   SELECT nome nome_completo FROM clientes; -- Funciona igual
   ```

2. Aliases são temporários e só existem durante a execução da consulta.
    
3. São especialmente úteis quando:
    
    - Você tem nomes de colunas longos
  
#### Linguagem SQL e Comandos DDL

É através da linguagem SQL que interagimos com o SGBD. Essa linguagem é composta de categorias de comandos. São elas DDL (comandos de definição de estruturas), DML (comandos de manipulação de dados, DCL (comandos de controle) e DQL (comandos de consulta).

Conhecer os comandos da linguagem SQL é fundamental para acessar o SGBD, manipular estruturas de armazenamento e seus dados.

**DDL – Data Definition Language – Trabalhando Com Tabelas**

A DDL é a parte da SQL usada para criar e manipular objetos que se relacionam aos dados, especialmente tabelas. Com a DDL você pode criar uma tabela, configurar suas colunas e todas as restrições de integridade, por isso antes de começarmos a escrever nossos primeiros comandos temos que entender bem a linguagem SQL e as restrições de integridade envolvidas.

A DDL está intimamente ligada também a modelagem física do banco de dados, pois é nessa parte do projeto onde os modelos lógicos são derivados para um banco de dados real, ou seja, se tornam físicos (saem do papel).

Vamos começar entendendo a sintaxe do comando que é capaz de criar uma tabela, o CREATE TABLE, que funciona da seguinte forma:

![[Pasted image 20250311090907.png]]

Para entender melhor este comando, vamos utilizá-lo em um modelo real. A modelagem conceitual pode ser vista na figura 1, onde estamos criando a base de dados de um pequeno jogo, onde cada personagem é de um tipo e possui um ou mais poderes (somente esta parte do jogo). A figura 2 mostra a derivação do respectivo contexto para a modelagem lógica.

![[Pasted image 20250311092519.png]]

Vamos começar a implementação física deste cenário pela tabela mais simples, ou seja, a que possui menos restrições e não depende de nenhuma outra tabela para existir. Neste caso temos as tabelas “tipo” e “poder”. A tabela “personagem”, por exemplo, possui uma chave estrangeira para “tipo” e, por isso, não poderíamos começar por ela, a não ser que façamos a inclusão da restrição referencial depois, alterando-a.

![[Pasted image 20250311092936.png]]

Repare que assim como na modelagem lógica, a restrição da chave primária recebe um nome, nesse caso “tipo_pk”. Isso ocorre nas restrições de chave e referencial. Ao se incluir a restrição de chave é necessário informar qual é a coluna que recebe essa restrição, neste caso a coluna “idTipo”. Seguindo a mesma lógica, criamos as próximas tabelas.

![[Pasted image 20250311093114.png]]

![[Pasted image 20250311093135.png]]

Repare na criação da tabela “personagem” que há a restrição referencial sendo aplicada com o acréscimo da CONSTRAINT do tipo FOREIGN KEY. Lembre-se que toda restrição, no Oracle, deve ter um nome e, no caso da chave estrangeira, é preciso informar qual coluna local a recebe e qual o “alvo”, ou seja, a tabela e sua respectiva coluna de chave primária.

Por fim, vamos criar a tabela de relacionamento entre “personagem” e “poder”, pois como a relação é N:N (cada personagem pode possuir N poderes e cada poder pode estar associado a N personagens), temos que as relacionar através de uma terceira tabela, conforme:

![[Pasted image 20250311093321.png]]

Repare nas quebras de linhas e a indentação (afastamento da margem) são diferentes para cada comando. Isso quer dizer que não importa se as linhas estão quebradas ou não para a execução do script, mas aqui são descritas assim para maior legibilidade. Essa é, inclusive, uma forte recomendação da comunidade internacional e de qualquer manual de bancos de dados. Repare, ainda, que todos os comandos foram escritos com letras maiúsculas e isso também poderia ter sido diferente, ou seja cada comando poderia ter sido escrito completamente em letras minúsculas, mas por boas práticas de programação escrevemos as palavras reservadas da SQL em letras maiúsculas e o nome dos objetos criados por nós mesmos em letras minúsculas. Por fim, e não menos importante, repare que ao final de cada comando há um “;” que especifica sua finalização.

Se você precisar excluir uma tabela, deve-se utilizar o comando “DROP TABLE nome_da_tabela;”, por exemplo “DROP TABLE tipo;” e a tabela tipo será eliminada do banco de dados. Deve-se utilizar este comando com muito cuidado.

Para se alterar dados de uma tabela, utiliza-se o comando “ALTER TABLE nome_da_tabela MODIFY (modificações);”. A palavra reservada “MODIFY” pode ser substituída por “ADD” se você está adicionando algo na tabela. Por exemplo, se você precisa alterar que a altura do personagem não pode ser nula, deve-se executar o comando “ALTER TABLE personagem MODIFY (altura NOT NULL);” e se você precisar acrescentar uma nova coluna chamada “idade” (que refere-se à idade da personagem), o comando “ALTER TABLE personagem ADD idade NUMBER(2) NULL;” deve ser executado.

Na criação de tabelas, usa-se um comando  DDL. Para criar uma tabela é necessário que o usuário tenha privilégio e uma área para armazenamento. A sintaxe simplificada para criação de tabelas é:


`**Sintaxe: CREATE TABLE** [_esquema._]_tabela_`
          `(nome da coluna _tipo do  dado_ [DEFAULT _expr_]`
              `_[constraint da coluna],_`
              `_...,_`
              `_[constraint da tabela]);_`

onde:

|   |   |
|---|---|
|_Esquema:_|é o  nome do proprietário da tabela, quando omitido a tabela é criada no esquema do usuário corrente|
|_Tabela:_|é o nome da tabela|
|_DEFAULT expr:_|especifica um valor default que será utilizado quando um dado for omitido na inserção|
|_Coluna:_|é o nome da coluna|
|_tipo de dados:_|é o tipo de dados e o comprimento da coluna|
|_Constraint:_|Está cláusula é opcional e especifica as restrições para a coluna ou para a tabela, quando o nome da constraint é omitido o Oracle assume uma identificação|

Convenções para Nomeação de Tabelas e Colunas:

• Deve começar com uma letra

• Pode ter de 1 a 30 caracteres (depende do SGBD)

• Deve conter somente A–Z, a–z, 0–9, _, $ e #

• Não deve duplicar o nome de outro objeto de propriedade do mesmo usuário

• Não deve ser uma palavra reservada pelo Oracle Server

Tipos de Dados:

![[Pasted image 20250311093856.png]]


No exemplo abaixo está sendo criada  a tabela DEPT, com três colunas — chamadas, DEPTNO, DNAME e LOC.

SQL>CREATE TABLE dept  
  2      (deptno NUMBER(2),

  3      dname          VARCHAR2(14),

  4      loc      VARCHAR2(13));

Table created.

A instrução Describe é utilizada para exibir a estrutura de uma tabela.

SQL> DESCRIBE dept

Name                Null?    Type

------------------ -------- ---------

DEPTNO                      NUMBER(2)

DNAME                       VARCHAR2(14)

LOC                         VARCHAR2(13)

---
**Restrições de Integridade**

São elas chaves primárias, chaves estrangeiras, colunas de dados únicos, não nulos etc., especialmente na modelagem lógica. Quando uma restrição é “violada” (não é atendida) é muito mais fácil encontrarmos a origem do erro. Os bancos de dados chamam as restrições com seu termo em inglês, ou seja, “CONSTRAINT”.

As restrições de integridade servem para impedir que dados inválidos sejam inseridos numa determinada coluna e são garantidas pelo próprio SGBD (Sistema Gerenciador de Banco de Dados), nós apenas as configuramos na hora de criar os objetos (através da DDL). Podemos, inclusive, dizer que as restrições (CONSTRAINTS) impõem regras nas colunas. Essas restrições são divididas em seis grupos, sendo:

- Restrição de integridade de **domínio**
- Restrição de integridade de **chave**
- Restrição de integridade **nula**
- Restrição de integridade **referencial**
- Restrição de integridade **unicidade**
- Restrição de integridade **de valor padrão**

A integridade de domínio especifica qual **tipo de valor** um determinado atributo pode admitir, ou seja, é são os tipos de dados (datatypes). Por exemplo, colunas configuradas como número inteiro, número de ponto flutuante, texto, data com hora, somente data, etc. Se um dado do tipo texto for inserido em uma coluna que aceita apenas valores numéricos, a restrição de integridade de domínio será violada. A integridade de domínio pode ir além, podendo **checar** se um valor inserido está dentro de uma especificação. Para isso, utiliza-se a restrição “CHECK”. Por exemplo, o estado no cadastro de um endereço, deve ser uma das 27 opções; o sexo de uma pessoa etc.

A integridade de vazio especifica se o valor de um atributo **pode ou não ser vazio**, ou seja, nulo. São os famosos NULL (permite que um dado seja vazio) e NOT NULL (não permite que um dado não seja especificado naquela coluna na hora de inserir uma linha). A integridade de vazio é também associada à cardinalidade mínima nos relacionamentos (0, a FK pode ser nula. 1, a FK não pode ser nula).

Já a integridade de chave (ou como alguns autores chamam, integridade de chave primária) garante que os valores das chaves primárias sejam sempre únicos e não nulos, pela própria definição de chave primária. Por exemplo, se tentarmos inserir uma linha cuja chave primária já exista, haverá violação da restrição de chave primária.

A integridade referencial é a integridade das FKs (chaves estrangeiras – _Foreign Keys_). Ela garante que o valor que aparecer nos atributos de uma chave estrangeira deve sempre aparecer na chave primária da tabela referenciada, ou seja, garante que todo valor de uma FK seja o mesmo de uma PK, a qual a coluna em questão aponta. Assim sendo, sempre que uma coluna é definida como FK, o SGBD deve garantir que ela sempre aponte para uma PK. Na hora que estamos criando as colunas FKs devemos dizer qual é a tabela alvo e sua respectiva chave primária.

A integridade de unicidade é aquela restrição que permite, ou não, que o valor se repita. No banco de dados utilizamos a palavra reservada UNIQUE quando queremos que seus dados sejam únicos, como por exemplo, o RG de uma pessoa, o e-mail de um usuário, os dados de uma impressão digital etc. Não confunda a restrição de unicidade com a de chave primária, pois os valores dessa coluna não são necessariamente identificadores da tabela.

Por fim e não menos importante temos a integridade de valor padrão associada à palavra reservada DEFAULT. Essa restrição permite que se um valor nulo for inserido em uma coluna (ou não foi informado, por exemplo) um valor padrão (pré-definido) é colocado em seu lugar. Por exemplo, se o país não foi informado numa tabela de endereços incluir “Brasil”. Essa restrição está fortemente ligada à restrição de nulo.

É muito importante reforçar que todas as restrições de integridade são garantidas pelo próprio SGBD. Uma restrição que não se encaixa em nenhuma das citadas aqui é chamada de restrição semântica e deve ser garantida pelo software que utiliza o banco de dados. Por exemplo, a cardinalidade máxima de um relacionamento ou, ainda como exemplo real, imagine que temos um relacionamento entre funcionários e departamento, onde um funcionário de recursos humanos não poderia assumir o cargo de analista de sistemas. Essa é uma restrição que deve ser garantida pela própria aplicação.

Pockt Guide

![[Pasted image 20250311095133.png]]

![[Pasted image 20250311095202.png]]

----

# Comandos DML  e DQL

**Introdução** 

É através da linguagem SQL que interagimos com o SGBD. Essa linguagem é composta de categorias de comandos. São elas DDL (comandos de definição de estruturas), DML (comandos de manipulação de dados, DCL (comandos de controle) e DQL (comandos de consulta).

Conhecer os comandos da linguagem SQL é fundamental para acessar o SGBD, manipular estruturas de armazenamento e seus dados.

**Comandos DML**

Os comandos da categoria DML (Data Manipulation Language), servem para realizar  adições, eliminações e atualizações em dados de um ou mais registros de uma ou mais tabelas de maneira concorrente. Os comandos da categoria DML são:

- Insert – Adição de linhas com  dados na tabela
- Update – Atualização de  dados na tabela
- Delete – Eliminação de dados da tabela
- Commit – Confirmação das transações, ou seja, salvamento dos dados
- Rollback – Desistência das transações, ou seja, desfazer a última transação

**A adição de linhas com dados é um comando DML.**

**Sintaxe:**

**INSERT INTO** _tabela_ [(_coluna_ [_, coluna..._])] **VALUES** _(valor_ [_, valor..._])_;_

Onde:

![](https://paperx-dex-assets.s3.sa-east-1.amazonaws.com/images/1693227350131-XB2TF5sprq.png)


### **Verificando a estrutura de uma tabela**

Para visualizar a ordem padrão das colunas e os tipos de dados esperados, utilize o comando `DESCRIBE`:

```
SQL> DESCRIBE dept;
```

📌 **Saída do comando:**

|Nome da Coluna|Permite Nulo?|Tipo de Dado|
|---|---|---|
|**DEPTNO**|NOT NULL|NUMBER(2)|
|**DNAME**|NULL|VARCHAR2(14)|
|**LOC**|NULL|VARCHAR2(13)|

🔹 O comando `DESCRIBE` exibe:

- A **ordem das colunas** na tabela.
- Se a coluna aceita valores **NULL**.
- O **tipo de dado** definido para cada campo.

💡 **Dica:** Sempre use `DESCRIBE` antes de inserir dados para garantir que os valores inseridos correspondam ao tipo esperado.


**Exemplo 1: Inserção completa com colunas especificadas**

```
SQL> INSERT INTO dept (DEPTNO, DNAME, LOC)  
  2  VALUES (80, 'COMERCIAL', 'SP');
```

🔹 Neste exemplo, estamos inserindo um novo departamento (**DEPTNO 80**) chamado **"COMERCIAL"**, localizado em **"SP"**.


**Exemplo 2: Inserção sem especificar colunas (assumindo a ordem da tabela)**

```
SQL> INSERT INTO dept  
  2  VALUES (90, 'FINANCEIRO', 'RJ');
```

🔹 Aqui, os valores estão sendo inseridos diretamente, assumindo que a tabela **`dept`** possui exatamente três colunas na ordem correta (**DEPTNO, DNAME e LOC**).

📌 **Recomendação:** Sempre que possível, especifique os nomes das colunas para evitar problemas caso a estrutura da tabela mude no futuro.

### **Inserção de Dados em Tabelas**


**Exemplo 3: Inserção parcial de dados**

```
SQL> INSERT INTO dept (deptno, dname)  
  2  VALUES (55, 'RH');
```

🔹 A tabela **`dept`** contém as colunas **`deptno`**, **`dname`** e **`loc`**.  
🔹 Como o campo **`loc`** não foi especificado, ele será preenchido automaticamente com **NULL**.


**Exemplo 4: Inserção com valor NULL explícito**

```
SQL> INSERT INTO dept  
  2  VALUES (45, 'DIRETORIA', NULL);
```

🔹 Aqui, os valores estão sendo inseridos diretamente, e o campo **`loc`** recebe **NULL** explicitamente.  
🔹 Isso é útil quando queremos deixar claro que o campo não terá um valor atribuído.


## **Inserção de Dados com Datas**

 **Exemplo 5: Inserindo um registro na tabela `emp`**

```
SQL> INSERT INTO emp  
  2  VALUES (3000, 'JOSE', 'VENDEDOR', 7782, TO_DATE('30/03/23', 'DD/MM/YY'),  
  3          2800, NULL, 20);
```

🔹 **Explicação dos valores inseridos:**

- `3000` → Código do empregado.
- `'JOSE'` → Nome do empregado.
- `'VENDEDOR'` → Cargo.
- `7782` → Código do gerente.
- `TO_DATE('30/03/23', 'DD/MM/YY')` → Data de admissão (convertida para formato de data).
- `2800` → Salário.
- `NULL` → Comissão (não aplicável).
- `20` → Código do departamento.

### **Visualizando os dados inseridos:**

Para verificar os registros na tabela **`emp`**, use:

```
SQL> SELECT *  
  2  FROM emp;
```

## **Atualização de Dados nos Registros**

**Sintaxe do comando `UPDATE`**

```
UPDATE tabela  
SET coluna = valor [, coluna = valor, ...]  
[WHERE condição];  
```

🔹 **Importante:** Se a cláusula `WHERE` for omitida, **todas as linhas** da tabela serão alteradas!

### **Exemplo: Atualizando um registro específico**

Atualizar o departamento para **30** do empregado com código **7900**:

```
SQL> UPDATE emp  
  2  SET deptno = 30  
  3  WHERE empno = 7900;
```

📌 **Sempre utilize a cláusula `WHERE` ao atualizar registros para evitar modificar toda a tabela por engano.**

### **Comando `SELECT`**

O comando `SELECT` é utilizado para realizar consultas aos dados armazenados em uma tabela.

**Exemplo de `SELECT` exibindo todos os dados da tabela `emp`**

```
SQL> SELECT *  
  2  FROM emp;
```

🔹 O asterisco (`*`) indica que **todas as colunas** da tabela serão retornadas na consulta.

## **Sintaxe do Comando `SELECT`**

🔹 **Regras para uso dos comandos SQL:**

- O SQL **não diferencia maiúsculas e minúsculas** no processamento dos comandos.
- Os comandos podem ser escritos em **uma ou mais linhas**.
- **Não é permitido abreviar** as palavras-chave dos comandos.
- **Escrever cada parte do comando em uma linha separada** melhora a legibilidade.
- Para exibir **apenas colunas específicas**, devemos nomeá-las na consulta.

 **Exemplo: Exibir apenas algumas colunas**
```
SQL> SELECT deptno, dname  
  2  FROM dept;
```

🔹 Aqui, estamos consultando apenas as colunas **`deptno`** (número do departamento) e **`dname`** (nome do departamento).

# **Operadores Aritméticos**

Os operadores aritméticos podem ser utilizados em qualquer cláusula de uma instrução SQL, **exceto na cláusula `FROM`**.

![[Pasted image 20250315082302.png]]

 **Exemplo: Exibir o salário original e o salário acrescido de R$ 300,00**

``` SQL
SQL> SELECT ename, sal, sal + 300  
  2  FROM emp;
```

![[Pasted image 20250315082338.png]]
➡️ **Nova coluna gerada apenas para exibição:** O resultado apresentará os nomes dos empregados (**`ename`**), seus salários originais (**`sal`**) e uma **coluna extra** mostrando os salários com um acréscimo de R$ 300,00.

### **Ordem de precedência matemática**

As regras matemáticas e a ordem de precedência continuam válidas dentro do SQL.

``` SQL
 SQL> SELECT ename, sal, sal + ((sal * 30) / 100)  
  2  FROM emp;
```

➡️ Aqui, estamos calculando o salário acrescido de **30%**.

✅ **Dica:** Use **parênteses** para garantir a ordem correta dos cálculos.

# **Operadores de Comparação**

Os operadores de comparação são utilizados para **estabelecer relações entre valores ou expressões**.

- O resultado de uma comparação é sempre um valor **booleano** (`TRUE` ou `FALSE`).
- Podem ser usados em **comparações que envolvem apenas uma linha**.

![[Pasted image 20250315082444.png]]

### **Operador `BETWEEN`**

Os valores especificados com `BETWEEN` são **inclusivos**. O limite **inferior** deve ser especificado primeiro.

```SQL
SQL> SELECT ename, sal  
  2  FROM emp  
  3  WHERE sal BETWEEN 1000 AND 1500;
```

➡️ Retorna os funcionários cujo salário está **entre R$ 1.000 e R$ 1.500** (inclusive).

### **Operador `IN`**

Verifica se um valor está presente em uma **lista de valores específicos**.

```SQL
SQL> SELECT empno, ename, mgr, deptno  
  2  FROM emp  
  3  WHERE ename IN ('FORD', 'ALLEN');
```

➡️ Retorna os funcionários cujo nome seja **"FORD"** ou **"ALLEN"**.

✅ Se forem utilizados **caracteres ou datas**, eles devem estar entre **aspas simples (`'`)**:

```SQL
SQL> SELECT empno, ename, mgr, deptno  
  2  FROM scott.emp  
  3  WHERE job IN ('PRESIDENT', 'MANAGER');
```

➡️ Retorna funcionários cujo cargo (`job`) seja **"PRESIDENT"** ou **"MANAGER"**.

### **Operador `LIKE`**

O operador `LIKE` permite buscar registros que **correspondam a um padrão de caracteres**.

```SQL 
SQL> SELECT ename  
  2  FROM scott.emp  
  3  WHERE ename LIKE 'J%';
```

➡️ Retorna todos os funcionários cujo nome começa com **"J"** (letra maiúscula).  
🔹 Se houver nomes iniciados com **"j" minúsculo**, eles **não serão retornados**.

✅ **Símbolos utilizados no `LIKE`**:

- `%` → Representa **qualquer sequência de caracteres**.
    - Exemplo: `'A%'` encontra **"Ana"**, **"Antonio"**, **"Alberto"**, etc.
- `_` → Representa **um único caractere**.
    - Exemplo: `'A_'` encontra **"Ao"**, **"An"**, mas não **"Ana"**.

---

### **Operador `IS NULL`**

Usado para verificar campos que **não possuem valor** (`NULL`).

```SQL
SQL> SELECT ename, job, deptno  
  2  FROM scott.emp  
  3  WHERE comm IS NULL;
```

➡️ Retorna os funcionários que **não recebem comissão** (`comm` está `NULL`).

✅ **Importante:** `NULL` significa **ausência de valor**.  
❌ **Não podemos usar `=` ou `!=` para comparar valores `NULL`**, pois `NULL` **não é igual nem diferente de nada**.

# **Operadores Lógicos**

Os operadores lógicos permitem combinar múltiplas condições para gerar um **único resultado**.  
✅ **Principais operadores lógicos no SQL:**

1. **`AND`** → Ambas as condições devem ser **verdadeiras**.
2. **`OR`** → Pelo menos **uma** das condições deve ser verdadeira.
3. **`NOT`** → Inverte o resultado da condição.

 **Exemplo: Filtrar funcionários com salário maior que 2000 e que pertencem ao departamento 30**

```SQL
SQL> SELECT ename, sal, deptno  
  2  FROM emp  
  3  WHERE sal > 2000 AND deptno = 30;
```

➡️ Apenas os funcionários do **departamento 30** com **salário superior a R$ 2.000** serão retornados.

# **Operadores Lógicos no SQL**

Os operadores lógicos são utilizados para **combinar expressões** na cláusula `WHERE`. Eles podem ser aplicados em **consultas (`SELECT`)**, **atualizações (`UPDATE`)** e **exclusões (`DELETE`)** de dados.

## **Operador `AND`**

O operador `AND` retorna resultados **apenas quando todas as condições são verdadeiras**.

**Exemplo: Selecionar funcionários com salário ≥ 1100 e cargo `SALESMAN`**

```SQL
SQL> SELECT empno, ename, job, sal  
  2  FROM scott.emp  
  3  WHERE sal >= 1100 AND job = 'SALESMAN';
```

✅ **Resultado:**

``` 
EMPNO     ENAME      JOB        SAL  
7876      ADAMS      SALESMAN   1100  
7934      MILLER     SALESMAN   1300  
```

- Apenas os funcionários que atendem **ambas as condições** (`sal >= 1100` **E** `job = 'SALESMAN'`) são selecionados.
- Se qualquer condição for **falsa**, a linha não será incluída no resultado.

⚠️ **Cuidado com maiúsculas e minúsculas em valores alfanuméricos!**

- SQL **distingue letras maiúsculas e minúsculas**. No exemplo acima, `SALESMAN` deve estar em **maiúsculas**, caso contrário, nenhum resultado será retornado.

## **Operador `OR`**

O operador `OR` retorna resultados **quando pelo menos uma das condições for verdadeira**.

**Exemplo: Selecionar funcionários com salário ≥ 1100 ou cargo `SALESMAN`**

``` SQL
 SELECT empno, ename, job, sal  
  2  FROM emp  
  3  WHERE sal >= 1100 OR job = 'SALESMAN';
```

✅ **Resultado (parcial):**

```
EMPNO     ENAME     JOB         SAL  
7839      KING      PRESIDENT   5000  
7698      BLAKE     MANAGER     2850  
7782      CLARK     MANAGER     2450  
7566      JONES     MANAGER     2975  
7654      MARTIN    SALESMAN    1250  
...
```

- Se um funcionário **tiver salário ≥ 1100** **OU** **for `SALESMAN`**, ele será incluído no resultado.
- Funcionários que atendem **apenas uma das condições** também aparecem na consulta.

## **Operador `NOT`**

O operador `NOT` **inverte o resultado de uma condição**.

### **Exemplo: Selecionar funcionários que NÃO sejam `CLERK`, `MANAGER` ou `ANALYST`**

```
SQL> SELECT ename, job  
  2  FROM scott.emp  
  3  WHERE job NOT IN ('CLERK', 'MANAGER', 'ANALYST');
```

✅ **Resultado:**

```
ENAME      JOB  
KING       PRESIDENT  
MARTIN     SALESMAN  
ALLEN      SALESMAN  
TURNER     SALESMAN  
WARD       SALESMAN  
```

- **Apenas os funcionários que NÃO possuem os cargos listados** (`CLERK`, `MANAGER`, `ANALYST`) aparecem no resultado.

✅ **`NOT` pode ser combinado com outros operadores:**

```
... WHERE job   NOT IN ('SALESMAN', 'MANAGER');  -- Exclui SALESMAN e MANAGER  
... WHERE sal   NOT BETWEEN 2500 AND 5000;      -- Exclui salários entre 2500 e 5000  
... WHERE ename NOT LIKE '%S%';                 -- Exclui nomes que contenham "S"  
... WHERE comm  IS   NOT NULL;                  -- Seleciona funcionários com comissão  
```

# **Controle de Transações (COMMIT & ROLLBACK)**

As transações garantem que um conjunto de operações **DML** (`INSERT`, `UPDATE`, `DELETE`) seja executado corretamente no banco de dados.

### **Requisitos das transações:**

✔ **Consistência** → Os dados devem permanecer íntegros.  
✔ **Atomicidade** → Todas as operações devem ser concluídas com sucesso ou nenhuma será realizada.  
✔ **Integridade** → O banco de dados deve sempre manter um estado válido.

🚀 **Exemplo prático: Transferência de dinheiro**

1. Debita um valor da conta A (`UPDATE` na conta de origem).
2. Credita o mesmo valor na conta B (`UPDATE` na conta de destino).
3. **Se ambos os passos forem bem-sucedidos**, a transação é **confirmada (`COMMIT`)**.
4. **Se houver erro**, a transação é **desfeita (`ROLLBACK`)**.

---

## **COMMIT & ROLLBACK**

📌 **COMMIT** → Confirma as alterações no banco de dados de forma permanente.  
📌 **ROLLBACK** → Desfaz as alterações, retornando o banco ao estado anterior.

### **Eventos que finalizam uma transação:**

✅ **Quando um `COMMIT` ou `ROLLBACK` é emitido explicitamente.**  
✅ **Ao executar um comando DDL (`CREATE`, `ALTER`, `DROP`).**  
✅ **Se o usuário sair do sistema sem confirmar (`COMMIT`) ou cancelar (`ROLLBACK`).**  
✅ **Se houver falha no sistema, ocorre um `ROLLBACK` automático.**

---

**Exemplo: Alterar o departamento de um funcionário e confirmar a transação**

```
SQL> UPDATE emp  
  2  SET deptno = 10  
  3  WHERE empno = 7900;
```

➡️ **Antes do `COMMIT`**, a alteração está apenas na memória.

✅ **Para salvar definitivamente:**

```SQL
COMMIT;
```

✅ **Para desfazer a alteração antes do `COMMIT`:**

```SQL
ROLLBACK;
```

🔹 Se `ROLLBACK` for usado antes do `COMMIT`, **as alterações serão desfeitas**.

![[Pasted image 20250315084422.png]]

**Exemplo do comando rollback:** Excluir todas as linhas da tabela employees

![[Pasted image 20250315084451.png]]

Com o comando Rollback, a alteração provocada é desfeita e a versão original da tabela é restabelecida.

----
👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾👾
## Consulta com Funções de uma única Linha

É através da linguagem SQL que interagimos com o SGBD. Essa linguagem é composta de categorias de comandos. São elas DDL (comandos de definição de estruturas), DML (comandos de manipulação de dados, DCL (comandos de controle) e DQL (comandos de consulta).

Conhecer os comandos da linguagem SQL é fundamental para acessar o SGBD, manipular estruturas de armazenamento e seus dados.

**Resumo**
É possível realizar operações aritméticas entre os campos de uma tabela dentro do comando Select. Entenda que trata-se apenas de uma consulta, nenhum dado está sendo alterado. Veja o exemplo:

![[Pasted image 20250316074645.png]]

O comando acima calcula o salário anual dos funcionários. Com os Operadores aritméticos podemos realizar expressões aritméticas. Veja o exemplo:

![[Pasted image 20250316074749.png]]

Observe, que nessa consulta, é feito o cálculo do salário anual, o valor do bônus anual que corresponde a 40% do salário anual e o valor total com a soma do salário anual e o bônus.

----

### Consulta com Funções de uma única Linha

É através da linguagem SQL que interagimos com o SGBD. Essa linguagem é composta de categorias de comandos. São elas DDL (comandos de definição de estruturas), DML (comandos de manipulação de dados, DCL (comandos de controle) e DQL (comandos de consulta).

-> Revisando 

É através da linguagem SQL que interagimos com o SGBD. Essa linguagem é composta de categorias de comandos. São elas DDL (comandos de definição de estruturas), DML (comandos de manipulação de dados, DCL (comandos de controle) e DQL (comandos de consulta).
#### 1. DDL (Data Definition Language) - Linguagem de Definição de Dados

Comandos para definir a estrutura do banco de dados (criar, alterar e excluir objetos).

**Exemplos:**
``` SQL
-- Criar uma tabela
CREATE TABLE clientes (
    id INT PRIMARY KEY,
    nome VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    data_cadastro DATE DEFAULT CURRENT_DATE
);

-- Alterar uma tabela (adicionar coluna)
ALTER TABLE clientes ADD COLUMN telefone VARCHAR(20);

-- Excluir uma tabela
DROP TABLE clientes;

-- Criar um índice
CREATE INDEX idx_nome ON clientes(nome);

-- Criar uma view
CREATE VIEW clientes_ativos AS
SELECT * FROM clientes WHERE ativo = TRUE;
```
#### 2. DML (Data Manipulation Language) - Linguagem de Manipulação de Dados

Comandos para manipular os dados armazenados (inserir, atualizar, deletar).

**Exemplos:**

```SQL
-- Inserir dados
INSERT INTO clientes (id, nome, email) 
VALUES (1, 'João Silva', 'joao@email.com');

-- Atualizar dados
UPDATE clientes 
SET telefone = '11999998888' 
WHERE id = 1;

-- Deletar dados
DELETE FROM clientes 
WHERE id = 1;

-- Inserir múltiplos registros
INSERT INTO clientes (id, nome, email) VALUES
(2, 'Maria Souza', 'maria@email.com'),
(3, 'Carlos Lima', 'carlos@email.com');
```

#### 3. DQL (Data Query Language) - Linguagem de Consulta de Dados

Comandos para consultar dados (basicamente o SELECT).

**Exemplos:**

``` SQL
-- Consulta simples
SELECT * FROM clientes;

-- Consulta com filtro
SELECT nome, email FROM clientes 
WHERE data_cadastro > '2023-01-01';

-- Consulta com ordenação
SELECT * FROM clientes 
ORDER BY nome ASC;

-- Consulta com junção de tabelas
SELECT p.descricao, p.preco, c.nome 
FROM produtos p
JOIN clientes c ON p.cliente_id = c.id;

-- Consulta com agregação
SELECT COUNT(*) as total_clientes, 
       AVG(valor_compra) as media_compras
FROM clientes;
```

#### 4. DCL (Data Control Language) - Linguagem de Controle de Dados

Comandos para controlar acesso e permissões.

**Exemplos:**
``` SQL
-- Conceder permissão
GRANT SELECT, INSERT ON clientes TO usuario_app;

-- Revogar permissão
REVOKE DELETE ON clientes FROM usuario_app;

-- Conceder todas as permissões
GRANT ALL PRIVILEGES ON DATABASE meu_banco TO admin;

-- Criar um papel (role) e conceder permissões
CREATE ROLE leitura;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO leitura;
```

## Resumo das categorias:

|Categoria|Propósito|Comandos principais|
|---|---|---|
|DDL|Definir estrutura|CREATE, ALTER, DROP, TRUNCATE, RENAME|
|DML|Manipular dados|INSERT, UPDATE, DELETE, MERGE|
|DQL|Consultar dados|SELECT|
|DCL|Controle de acesso|GRANT, REVOKE, DENY|

Cada tipo de comando tem um propósito específico no gerenciamento e manipulação de bancos de dados relacionais.

### Apelidos (Aliases) em SQL

Os apelidos (ou aliases) em SQL são "apelidos" temporários que você pode atribuir a tabelas ou colunas em suas consultas para tornar o código mais legível ou mais fácil de escrever. Eles são muito úteis em consultas complexas.

### 1. Aliases para Colunas

Usados para renomear colunas nos resultados da consulta.

**Sintaxe:**
```SQL
SELECT 
    nome AS nome_completo,
    email AS endereco_eletronico,
    data_cadastro AS cadastro
FROM clientes;
```

Usados para simplificar referências a tabelas, especialmente em junções.

**Sintaxe:**
```SQL
SELECT 
    c.nome,
    p.descricao
FROM clientes AS c
JOIN pedidos AS p ON c.id = p.cliente_id;
```

1. A palavra-chave `AS` é opcional:
  ```SQL
   SELECT nome nome_completo FROM clientes; -- Funciona igual
   ```
   
2. Aliases são temporários e só existem durante a execução da consulta.
    
3. São especialmente úteis quando:
    
    - Você tem nomes de colunas longos
  
    - Trabalha com múltiplas tabelas
    
    - Usa funções ou expressões nas colunas
    
    - Há colunas com nomes iguais em tabelas diferentes
    
4. Para apelidos que contenham espaços ou caracteres especiais, use aspas:
```SQL
SELECT nome AS "Nome Completo" FROM clientes;
```

## Exemplos avançados:

**Com funções:**
```SQL
SELECT 
    AVG(salario) AS media_salarial,
    COUNT(*) AS total_funcionarios
FROM empregados;
```

**Com expressões:**
```SQL
SELECT 
    nome || ' ' || sobrenome AS nome_completo,
    salario * 12 AS salario_anual
FROM funcionarios;
```

➡️ versão alternativa com MySQL
```MySQL
SELECT 
    CONCAT(nome, ' ', sobrenome) AS nome_completo,
    salario * 12 AS salario_anual
FROM funcionarios;
```

**Com múltiplas tabelas (muito comum):**
```SQL
SELECT 
    p.nome AS produto,
    f.nome AS fabricante,
    p.preco AS preco_unitario
FROM produtos AS p
JOIN fabricantes AS f ON p.fabricante_id = f.id;
```

**Em subconsultas:**
```SQL
SELECT 
    d.nome AS departamento,
    sub.media AS media_salarial
FROM departamentos d
JOIN (
    SELECT 
        departamento_id, 
        AVG(salario) AS media
    FROM empregados
    GROUP BY departamento_id
) AS sub ON d.id = sub.departamento_id;
```

Os aliases são uma ferramenta poderosa para tornar suas consultas SQL mais claras e fáceis de manter, especialmente em consultas complexas com múltiplas tabelas e junções.

### **Funções de Linha Única (Single-Row Functions) em SQL**
As **funções de linha única** são funções SQL que operam em **cada registro individualmente**, retornando um resultado para cada linha processada. Elas são aplicadas a **valores de colunas** e podem ser usadas em consultas `SELECT`, `WHERE`, `ORDER BY` e outras cláusulas.

## **Categorias de Funções de Linha Única**

### **1. Funções de Texto (String Functions)**

Manipulam dados do tipo **CHAR, VARCHAR, TEXT**.

|Função|Descrição|Exemplo|Resultado|
|---|---|---|---|
|`UPPER(texto)`|Converte para maiúsculas|`UPPER('sql')`|`SQL`|
|`LOWER(texto)`|Converte para minúsculas|`LOWER('SQL')`|`sql`|
|`INITCAP(texto)`|Primeira letra maiúscula (Oracle, PostgreSQL)|`INITCAP('sql server')`|`Sql Server`|
|`LENGTH(texto)`|Retorna o tamanho do texto|`LENGTH('Banco de Dados')`|`13`|
|`SUBSTR(texto, start, length)`|Extrai parte de uma string|`SUBSTR('SQL Server', 5, 6)`|`Server`|
|`REPLACE(texto, old, new)`|Substitui parte de uma string|`REPLACE('SQL Server', 'SQL', 'MySQL')`|`MySQL Server`|
|`CONCAT(str1, str2)`|Concatena strings|`CONCAT('SQL', ' Server')`|`SQL Server`|
|`TRIM(texto)`|Remove espaços em branco no início e no fim|`TRIM(' SQL ')`|`SQL`|

---

### **2. Funções Numéricas (Numeric Functions)**

Operam em valores **INT, FLOAT, DECIMAL**.

|Função|Descrição|Exemplo|Resultado|
|---|---|---|---|
|`ROUND(num, dec)`|Arredonda um número|`ROUND(15.78, 1)`|`15.8`|
|`TRUNC(num, dec)`|Trunca (corta) casas decimais|`TRUNC(15.78, 1)`|`15.7`|
|`CEIL(num)`|Arredonda para cima (menor inteiro >= num)|`CEIL(15.2)`|`16`|
|`FLOOR(num)`|Arredonda para baixo (maior inteiro <= num)|`FLOOR(15.9)`|`15`|
|`MOD(num1, num2)`|Retorna o resto da divisão|`MOD(10, 3)`|`1`|
|`ABS(num)`|Retorna o valor absoluto|`ABS(-15)`|`15`|
|`POWER(num, exp)`|Eleva um número a uma potência|`POWER(2, 3)`|`8`|

---

### **3. Funções de Data (Date Functions)**

Manipulam valores **DATE, TIMESTAMP**.

|Função|Descrição|Exemplo (Oracle)|Resultado|
|---|---|---|---|
|`SYSDATE` / `NOW()`|Retorna a data e hora atuais|`SELECT SYSDATE FROM dual;`|`2023-10-25 14:30:00`|
|`TO_CHAR(data, formato)`|Converte data para texto formatado|`TO_CHAR(SYSDATE, 'DD/MM/YYYY')`|`25/10/2023`|
|`TO_DATE(texto, formato)`|Converte texto para data|`TO_DATE('25-10-2023', 'DD-MM-YYYY')`|`2023-10-25`|
|`MONTHS_BETWEEN(data1, data2)`|Calcula meses entre duas datas (Oracle)|`MONTHS_BETWEEN('25-OCT-2023', '25-JAN-2023')`|`9`|
|`ADD_MONTHS(data, meses)`|Adiciona meses a uma data (Oracle)|`ADD_MONTHS(SYSDATE, 3)`|`2024-01-25`|
|`LAST_DAY(data)`|Retorna o último dia do mês|`LAST_DAY(SYSDATE)`|`2023-10-31`|

---

### **4. Funções de Conversão (Conversion Functions)**

Convertem um tipo de dado em outro.

|Função|Descrição|Exemplo|Resultado|
|---|---|---|---|
|`TO_CHAR(num/data)`|Converte número/data para texto|`TO_CHAR(1500, '$9999')`|`$1500`|
|`TO_NUMBER(texto)`|Converte texto para número|`TO_NUMBER('1500')`|`1500`|
|`CAST(valor AS tipo)`|Conversão genérica|`CAST('2023-10-25' AS DATE)`|`2023-10-25`|

---

### **5. Funções Condicionais (Conditional Functions)**

Retornam valores com base em condições.

|Função|Descrição|Exemplo (Oracle)|Resultado|
|---|---|---|---|
|`NVL(valor, substituto)`|Se `valor` for NULL, retorna `substituto`|`NVL(salario, 0)`|`0` (se salario for NULL)|
|`COALESCE(val1, val2, ...)`|Retorna o primeiro valor não-NULL|`COALESCE(telefone, celular, 'Sem contato')`|`'Sem contato'` (se ambos forem NULL)|
|`DECODE` (Oracle) / `CASE`|Estrutura condicional|`CASE WHEN salario > 5000 THEN 'Alto' ELSE 'Baixo' END`|`'Alto'` ou `'Baixo'`|

---
**Exemplo:**
```SQL
SELECT 
    nome,
    UPPER(sobrenome) AS sobrenome_maiusculo,
    salario,
    ROUND(salario * 1.10, 2) AS salario_com_aumento,
    TO_CHAR(data_contratacao, 'DD/MM/YYYY') AS data_formatada,
    NVL(telefone, 'Não informado') AS telefone
FROM funcionarios
WHERE LENGTH(nome) > 5
ORDER BY salario DESC;
```

**Resultado:**

|nome|sobrenome_maiusculo|salario|salario_com_aumento|data_formatada|telefone|
|---|---|---|---|---|---|
|João|SILVA|5000|5500.00|15/03/2020|(11) 9999-8888|
|Maria|SANTOS|4500|4950.00|20/05/2021|Não informado|

# **Funções de Conversão de Data em SQL**

As funções de conversão de data são essenciais para manipular e formatar valores temporais em bancos de dados. Elas permitem transformar:

- **Strings em datas** (para armazenamento ou filtro)
    
- **Datas em strings** (para exibição amigável)
    
- **Entre formatos de data/hora** (timestamp → date, etc.)

##### **Principais funções:**

**`MONTHS_BETWEEN(data1, data2)`**  
Calcula o número de meses entre duas datas (pode retornar valor fracionário).
```SQL
SELECT MONTHS_BETWEEN('15-JAN-2025', '15-MAR-2024') FROM dual;
-- Retorno: 10 (meses entre as datas)
```

**`ADD_MONTHS(data, n)`**  
Adiciona ou subtrai meses a uma data.
```SQL
SELECT ADD_MONTHS('01-JAN-2024', 3) FROM dual;
-- Retorno: 01-APR-2024
```

**`LAST_DAY(data)`**  
Retorna o último dia do mês da data especificada.
```SQL
SELECT LAST_DAY('10-FEB-2024') FROM dual;
-- Retorno: 29-FEB-2024 (2024 é bissexto)
```

**`NEXT_DAY(data, 'dia_semana')`**  
Encontra a próxima ocorrência de um dia da semana após a data.
```SQL
SELECT NEXT_DAY('01-MAR-2024', 'SEGUNDA') FROM dual;
-- Retorno: 04-MAR-2024 (próxima segunda-feira)
```

#### Funções para Conversão de Dados**

### **Principais funções:**

**`TO_CHAR(data|número, formato)`**  
Converte datas ou números para texto formatado.
```SQL
SELECT TO_CHAR(SYSDATE, 'DD/MM/YYYY HH24:MI') FROM dual;
-- Retorno: "24/03/2024 14:30"
```

**`TO_DATE(texto, formato)`**  
Converte texto em data.
```SQL
SELECT TO_DATE('25-Dez-2024', 'DD-Mon-YYYY') FROM dual;
-- Retorno: 25/12/2024 (como valor DATE)
```

**`TO_NUMBER(texto, formato)`**  
Converte texto em número.
```SQL
SELECT TO_NUMBER('1.250,50', '9G999D99') FROM dual;
-- Retorno: 1250.5 (como valor numérico)
```

#### **Conversão de Datas em Caracteres**

**Formatos mais usados com TO_CHAR:**

|Código|Descrição|Exemplo de Saída|
|---|---|---|
|`DD`|Dia do mês (01-31)|15|
|`MM`|Mês (01-12)|03|
|`YYYY`|Ano com 4 dígitos|2024|
|`DAY`|Nome completo do dia|"SEGUNDA-FEIRA"|
|`MON`|Nome abreviado do mês|"MAR"|
|`HH24`|Hora no formato 24h|14|
|`MI`|Minutos|30|

#### **Função NVL**
Substitui valores NULL por um valor padrão especificado.

**Sintaxe:**
```SQL
NVL(valor, valor_se_null)
```

**Casos de uso:**
1. Evitar erros em cálculos com NULL
2. Melhorar a apresentação de dados em relatórios

**Exemplos:**
Substituição de NULL por 0 em comissões
```SQL
-- Substituir NULL por 0 em comissões
SELECT 
    nome,
    salario,
    NVL(comissao, 0) AS comissao_ajustada,
    salario + NVL(comissao, 0) AS total
FROM vendedores;

-- Substituir NULL por texto
SELECT 
    nome,
    NVL(email, 'E-mail não cadastrado') AS contato
FROM clientes;
```

**Resultado (tabela fictícia):**

|NOME|SALARIO|COMISSAO_AJUSTADA|TOTAL|
|---|---|---|---|
|João|2500|300|2800|
|Maria|1800|0|1800|
|Carlos|2200|150|2350|
|Ana|3000|500|3500|
|Pedro|2000|0|2000|

**Observação:** Maria e Pedro tinham NULL na coluna comissao, que foram substituídos por 0.

Substituição de NULL por texto
```SQL
SELECT 
    nome,
    NVL(email, 'E-mail não cadastrado') AS contato
FROM clientes;
```

**Resultado (tabela fictícia):**

|NOME|CONTATO|
|---|---|
|Ana|[ana@empresa.com](https://mailto:ana@empresa.com/)|
|Luiz|E-mail não cadastrado|
|Carla|[carla.silva@email.com](https://mailto:carla.silva@email.com/)|
|Marcos|E-mail não cadastrado|
|Fernanda|[fernanda@outlook.com](https://mailto:fernanda@outlook.com/)|
**Observação:** Luiz e Marcos tinham NULL na coluna email, que foram substituídos pelo texto padrão.

 
 Exemplo com COALESCE
 ```SQL
 SELECT 
    nome,
    COALESCE(comissao, bonus, 0) AS remuneracao_variavel
FROM vendedores;
```

**Resultado (tabela fictícia):**

|NOME|REMUNERACAO_VARIAVEL|
|---|---|
|João|300|
|Maria|100|
|Carlos|150|
|Ana|500|
|Pedro|0|

**Observação:**

- João, Carlos e Ana tinham valores em 'comissao'
    
- Maria tinha NULL em 'comissao' mas 100 em 'bonus'
    
- Pedro tinha NULL em ambas colunas, retornando 0
    

## Diferença entre NVL e COALESCE

|Função|Vantagens|Limitações|
|---|---|---|
|NVL|Simples, presente em todos os bancos|Só trabalha com 2 argumentos|
|COALESCE|Aceita múltiplos argumentos|Não suportado em bancos muito antigos|

COALESCE é particularmente útil quando você tem várias colunas alternativas que podem conter valores nulos.

# extra
questões 
```SQL
SELECT TO_CHAR(price, '$999990.99')
FROM inventory;
```

- `TO_CHAR` é a função válida para formatar números como strings no Oracle e outros bancos SQL

 Formato monetário adequado:
- `'$999990.99'` é um formato que:
- Mostra o símbolo de dólar (`$`)
- Permite até 5 dígitos antes do ponto (`99999`)
-  Mostra sempre 2 casas decimais (`.99`)
- Inclui um `0` extra para garantir que o número `0` seja mostrado como `$0.00` (ao invés de apenas `$.00`)
---

# Joins 

**Uso da Cláusula ON para estabelecer a condição de Junção**

A condição da junção natural é basicamente uma equijunção de todas as campos com o mesmo nome. Para especificar condições arbitrárias ou campos a serem unidas, é usada a cláusula ON. A condição de junção é separada de outras condições de pesquisa. A cláusula ON facilita a compreensão do código.

## **1. Conceito Fundamental: Por que precisamos de junções?**

Quando dados estão distribuídos em várias tabelas (normalização), usamos **junções** para combiná-los de forma lógica.

**Exemplo Prático:**

- Tabela `EMP` (funcionários): contém `EMPNO`, `ENAME`, `DEPTNO`

- Tabela `DEPT` (departamentos): contém `DEPTNO`, `DNAME`, `LOC`


Precisamos mostrar o nome do funcionário **junto com** seu departamento e localização.

---
#### **2. Como Funciona uma Junção? (Passo a Passo)**

Imagine as tabelas assim:

**Tabela EMP:**

|EMPNO|ENAME|DEPTNO|
|---|---|---|
|7369|SMITH|20|
|7499|ALLEN|30|
|7521|WARD|30|

**Tabela DEPT:**

|DEPTNO|DNAME|LOC|
|---|---|---|
|10|ACCOUNTING|NEW YORK|
|20|RESEARCH|DALLAS|
|30|SALES|CHICAGO|

### **Processo de Junção:**

1. O SQL pega o primeiro registro da tabela `EMP` (SMITH, DEPTNO=20)
2. Procura em `DEPT` onde `DEPTNO=20`
3. Encontra "RESEARCH, DALLAS"
4. Combina os dados:
==SMITH (do EMP) + RESEARCH/DALLAS (do DEPT)==
5. Repete para todos os registros.

#### **3. Tipos de Junções**

 ## a)**INNER JOIN (Junção Interna)**

**O que faz?**  
Retorna **apenas** os registros que têm correspondência em AMBAS as tabelas.

**Sintaxe:**
```SQL
SELECT colunas
FROM tabela1
INNER JOIN tabela2 ON tabela1.chave = tabela2.chave
```

**Exemplo:**
```SQL
SELECT E.ENAME, D.DNAME, D.LOC
FROM EMP E
INNER JOIN DEPT D ON E.DEPTNO = D.DEPTNO;
```

**Resultado:**

| ENAME | DNAME    | LOC     |
| ----- | -------- | ------- |
| SMITH | RESEARCH | DALLAS  |
| ALLEN | SALES    | CHICAGO |
| WARD  | SALES    | CHICAGO |

Se um funcionário tiver `DEPTNULL` ou um `DEPTNO` que não existe em `DEPT`, ele **não aparecerá** no resultado.

-----

 **b) LEFT JOIN (Junção à Esquerda)**

**O que faz?**  
Retorna **TODOS** os registros da tabela à esquerda (`EMP`), mesmo sem correspondência em `DEPT`.

**Exemplo:**
```SQL
SELECT E.ENAME, D.DNAME
FROM EMP E
LEFT JOIN DEPT D ON E.DEPTNO = D.DEPTNO;
```

**Se existir um funcionário sem departamento:**

| ENAME | DNAME    |                                |
| ----- | -------- | ------------------------------ |
| SMITH | RESEARCH |                                |
| ALLEN | SALES    |                                |
| WARD  | SALES    |                                |
| JONES | NULL     | ← Funcionário sem departamento |

---

 **c) RIGHT JOIN (Junção à Direita)**

**O que faz?**  
Retorna **TODOS** os registros da tabela à direita (`DEPT`), mesmo sem funcionários.

**Exemplo:**
```SQL
SELECT E.ENAME, D.DNAME
FROM EMP E
RIGHT JOIN DEPT D ON E.DEPTNO = D.DEPTNO;
```

**Se existir um departamento sem funcionários:**

|ENAME|DNAME|
|---|---|
|SMITH|RESEARCH|
|ALLEN|SALES|
|WARD|SALES|
|NULL|ACCOUNTING|← Departamento sem funcionários|

---

 **d) FULL JOIN (Junção Completa)**

**O que faz?**  
Retorna **TODOS** os registros de ambas as tabelas, combinando onde possível.

**Exemplo:**
```SQL
SELECT E.ENAME, D.DNAME
FROM EMP E
FULL JOIN DEPT D ON E.DEPTNO = D.DEPTNO;
```

**Resultado hipotético:**

| ENAME | DNAME      |                                 |
| ----- | ---------- | ------------------------------- |
| SMITH | RESEARCH   |                                 |
| ALLEN | SALES      |                                 |
| WARD  | SALES      |                                 |
| JONES | NULL       | ← Funcionário sem departamento  |
| NULL  | ACCOUNTING | ← Departamento sem funcionários |

---

 **4. Autojunção (SELF JOIN)**

**Quando usar?**  
Quando uma tabela referencia a si mesma (ex.: tabela de funcionários onde cada um tem um gerente).

**Estrutura da Tabela:**

| EMPNO | ENAME | MGR  |                              |
| ----- | ----- | ---- | ---------------------------- |
| 7369  | SMITH | 7902 |                              |
| 7499  | ALLEN | 7698 |                              |
| 7902  | FORD  | NULL | ← Presidente não tem gerente |

**Consulta:**
```SQL
SELECT F.ENAME AS FUNCIONARIO, G.ENAME AS GERENTE
FROM EMP F
LEFT JOIN EMP G ON F.MGR = G.EMPNO;
```

**Resultado:**

| FUNCIONARIO | GERENTE |                   |
| ----------- | ------- | ----------------- |
| SMITH       | FORD    |                   |
| ALLEN       | BLAKE   |                   |
| FORD        | NULL    | ← Não tem gerente |

 **5. Erros Comuns e Como Evitá-los**

### **Problema 1: Coluna Ambígua**

**Mensagem:**  
`ORA-00918: column ambiguously defined`

**Causa:**  
Duas tabelas têm colunas com o mesmo nome (ex.: `DEPTNO` em `EMP` e `DEPT`).

**Solução:**  
Sempre prefixe com o nome/apelido da tabela:
```SQl
-- ERRADO (ambíguo)
SELECT DEPTNO FROM EMP JOIN DEPT ON... 

-- CORRETO
SELECT EMP.DEPTNO, DEPT.DNAME 
FROM EMP JOIN DEPT ON EMP.DEPTNO = DEPT.DEPTNO;
```

 **Problema 2: Junção Incorreta**

**Causa:**  
Usar `WHERE` em vez de `ON` para junções.

**Solução:**
```SQL
-- ERRADO (filtra após a junção)
SELECT * FROM EMP, DEPT WHERE EMP.DEPTNO = DEPT.DEPTNO;

-- CORRETO (junção explícita)
SELECT * FROM EMP INNER JOIN DEPT ON EMP.DEPTNO = DEPT.DEPTNO;
```

## **Resumo Visual das Junções**

| Tipo de Junção | Retorna                                 | Sintaxe SQL                       |
| -------------- | --------------------------------------- | --------------------------------- |
| **INNER JOIN** | Apenas correspondências                 | `FROM A INNER JOIN B ON A.x=B.y`  |
| **LEFT JOIN**  | Tudo de A + correspondências em B       | `FROM A LEFT JOIN B ON A.x=B.y`   |
| **RIGHT JOIN** | Tudo de B + correspondências em A       | `FROM A RIGHT JOIN B ON A.x=B.y`  |
| **FULL JOIN**  | Tudo de ambas, combinando onde possível | `FROM A FULL JOIN B ON A.x=B.y`   |
| **SELF JOIN**  | Junção da tabela com ela mesma          | `FROM A X JOIN A Y ON X.pai=Y.id` |

**Junções Externas – OuterJoin**

Caso um registro não satisfizer uma condição de junção, o registro não aparecere no relatório da consulta. Por exemplo, na equijoin das tabelas EMP e DEPT, o departamento 40 OPERATIONS não aparece porque nenhum empregado trabalha neste departamento. Os registros ausentes, podem ser regastados, caso um operador de _outerjoin_ seja usado na condição de junção.

![[Pasted image 20250324165451.png]]

O Outer Join é um tipo de junção em SQL que permite incluir no resultado **todos os registros de uma tabela**, mesmo quando não há correspondência na outra tabela. É extremamente útil quando você precisa:

- Manter todos os registros de uma tabela principal
    
- Incluir informações relacionadas quando existirem
    
- Identificar registros "órfãos" (sem relacionamento)

## **Quando Usar Cada Tipo?**

|Tipo|Quando Usar|Exemplo Comum|
|---|---|---|
|**LEFT JOIN**|Quando você quer todos os registros da tabela principal, mesmo sem relação|Todos os clientes, com ou sem pedidos|
|**RIGHT JOIN**|Quando você quer todos os registros da tabela secundária, mesmo sem relação|Todos os produtos, mesmo não vendidos|
|**FULL JOIN**|Quando precisa de todos os registros de ambas tabelas|Relatório completo de relacionamentos|

## **Diferença Crucial: Outer Join vs Inner Join**
```SQL
-- Inner Join (apenas correspondências)
SELECT E.ename, D.dname
FROM emp E
INNER JOIN dept D ON E.deptno = D.deptno;

-- Left Outer Join (todos os empregados)
SELECT E.ename, D.dname
FROM emp E
LEFT JOIN dept D ON E.deptno = D.deptno;
```

```SQL
-- INNER JOIN
ENAME   DNAME
------  --------
SMITH   RESEARCH
ALLEN   SALES
WARD    SALES

-- LEFT JOIN
ENAME   DNAME
------  --------
SMITH   RESEARCH
ALLEN   SALES
WARD    SALES
JONES   NULL     ← Aparece no LEFT mas não no INNER
```

# Auto Join em SQL:
O Auto Join (ou "Self Join") é uma técnica poderosa em SQL que permite **juntar uma tabela a si mesma**. É especialmente útil quando você precisa:

- Analisar relações hierárquicas (como gerentes-subordinados)
- Comparar registros dentro da mesma tabela
- Encontrar relacionamentos entre entidades do mesmo tipo

## **Como Funciona o Auto Join?**

Imagine uma tabela de funcionários onde cada registro sabe quem é seu gerente:

### **Estrutura da Tabela EMP**

|EMPNO|ENAME|JOB|MGR|DEPTNO|
|---|---|---|---|---|
|7839|KING|PRESIDENT|NULL|10|
|7698|BLAKE|MANAGER|7839|30|
|7782|CLARK|MANAGER|7839|10|
|7566|JONES|MANAGER|7839|20|
|7499|ALLEN|SALESMAN|7698|30|

Note que:

- `MGR` (Manager) é o `EMPNO` do gerente
- KING não tem gerente (`MGR` é NULL)

```SQL
SELECT a.coluna1, b.coluna2
FROM tabela a
JOIN tabela b ON a.chave = b.chave_relacionada
```

## **Exemplo Prático 1: Hierarquia de Gerência**

```SQL
SELECT 
   e.ename AS funcionario,
   m.ename AS gerente
FROM 
   emp e
LEFT JOIN 
   emp m ON e.mgr = m.empno;
```

**Resultado:**

|FUNCIONARIO|GERENTE|
|---|---|
|BLAKE|KING|
|CLARK|KING|
|JONES|KING|
|ALLEN|BLAKE|
|KING|NULL|

👉 **Observe que**:

- Usamos `LEFT JOIN` para incluir KING (que não tem gerente)
    
- A tabela `emp` é referenciada duas vezes com aliases diferentes (`e` e `m`)
    

## **Exemplo Prático 2: Encontrar Colegas de Departamento**

```SQL
SELECT 
   a.ename AS funcionario1,
   b.ename AS funcionario2,
   a.deptno
FROM 
   emp a
JOIN 
   emp b ON a.deptno = b.deptno AND a.empno < b.empno;
```

**Resultado:**

|FUNCIONARIO1|FUNCIONARIO2|DEPTNO|
|---|---|---|
|BLAKE|ALLEN|30|
|CLARK|KING|10|

👉 **Por que `a.empno < b.empno`?**  
Evita duplicatas (ex: "BLAKE-ALLEN" e "ALLEN-BLAKE")

#### **Casos de Uso Comuns**

1. **Estruturas Hierárquicas**:

- Organogramas empresariais

- Estruturas de pastas em sistemas de arquivos
   
2. **Relacionamentos Recursivos**:

- Amizades em redes sociais

- Componentes que usam outros componentes

3. **Análise Comparativa**:

- Comparar vendas entre vendedores da mesma região

- Identificar produtos similares

#### **Diferença Entre Auto Join e Junções Tradicionais**

|Característica|Auto Join|Junção Tradicional|
|---|---|---|
|Tabelas envolvidas|Mesma tabela (2 alias)|Tabelas diferentes|
|Propósito principal|Analisar relações internas|Relacionar dados distintos|
|Complexidade|Maior cuidado com alias|Mais intuitiva|

## **Dicas de Performance**

1. **Use índices** nas colunas de junção
2. **Filtre cedo** com WHERE quando possível
3. **Evite SELECT *** - liste apenas as colunas necessárias

-----
## Funções de Grupo e Subconsultas

Uma subconsulta é uma  consulta utilizada dentro de uma instrução SQL. Pode ser utilizada dentro de instruções select, insert, delete update ou create table.

### **Funções de Grupo em SQL**

As funções de grupo operam em conjuntos de linhas para fornecer um resultado por grupo. Essas operações podem envolver:

- Todas as linhas de uma tabela, ou
    
- Conjuntos de linhas definidos por critérios pré-estabelecidos.
    

Assim como em outras linguagens ou aplicativos, as funções SQL requerem argumentos (representados pelo nome da coluna) e retornam valores. A sintaxe básica é:

```SQL
FUNÇÃO(coluna)
```

---

### **Funções Disponíveis**

|Função|Descrição|
|---|---|
|`AVG()`|Retorna a média dos valores de um conjunto.|
|`COUNT()`|Retorna a quantidade de ocorrências.|
|`MAX()`|Retorna o maior valor de um conjunto.|
|`MIN()`|Retorna o menor valor de um conjunto.|
|`SUM()`|Retorna a somatória dos valores.|
|`VARIANCE()`|Retorna a variância entre os valores.|

---
**Sintaxe Completa**

```SQL
SELECT [coluna,] função_de_grupo(coluna)
FROM tabela
[WHERE condição]
[GROUP BY coluna]
[HAVING condição]
[ORDER BY coluna];
```
#### **Explicação das Cláusulas**

- **`[coluna,]`**: Lista opcional de colunas envolvidas na consulta.
    
- **`função_de_grupo(coluna)`**: Função aplicada aos dados da coluna especificada.
    
- **`FROM tabela`**: Tabela(s) consultada(s).
    
- **`WHERE condição`**: Filtra linhas antes do agrupamento.
    
- **`GROUP BY coluna`**: Agrupa os dados pela coluna especificada.
    
- **`HAVING condição`**: Filtra grupos (similar ao `WHERE`, mas para colunas agrupadas).
    
- **`ORDER BY coluna`**: Ordena os resultados (ascendente por padrão).

---
### **Observações Importantes**

1. **Valores Nulos**:
    
    - Todas as funções de grupo (exceto `COUNT(*)`) ignoram valores nulos.

    - Para substituir valores nulos, use a função `NVL`.

2. **Agrupamento Simples**:
    
    - Envolve todas as linhas de uma tabela que satisfazem um critério.
    
    - Cada função produz um único resultado para o conjunto.

---
![[Pasted image 20250402082200.png]]

### **Exemplos de Funções de Grupo em SQL**

 **Exemplo 1: Maior Salário da Tabela**

**Objetivo**: Retornar o maior salário entre todos os funcionários.

- Avalia todas as linhas da tabela e retorna um único valor.

```SQL
SELECT MAX(sal) AS "Maior Salário"
FROM scott.EMP;
```
**Saída**:
```SQL
Maior Salário
-------------
        5000
```

 **Exemplo 2: Estatísticas Salariais por Cargo**

**Objetivo**: Calcular a média, o maior/menor salário e a soma dos salários para funcionários do departamento **SALES**.

```SQL
SELECT 
    AVG(sal) AS "Média Salarial",
    MAX(sal) AS "Maior Salário",
    MIN(sal) AS "Menor Salário",
    SUM(sal) AS "Total Folha de Pagamento"
FROM scott.emp
WHERE job LIKE 'SALES%';
```
**Saída**
```SQL
Média Salarial | Maior Salário | Menor Salário | Total Folha de Pagamento
---------------|---------------|---------------|-------------
1400           | 1600          | 1250          | 5600
```

 **Exemplo 3: Contagem de Funcionários por Departamento**

**Objetivo**: Contar quantos funcionários trabalham no departamento **30**.

```SQL
SELECT COUNT(*) AS "Total de Funcionários"
FROM scott.emp
WHERE deptno = 30;
```
**Saída**
```SQL
Total de Funcionários
---------------------
6
```
**Diferença entre `COUNT(*)` e `COUNT(expr)`**

|Função|Descrição|
|---|---|
|**`COUNT(*)`**|Conta **todas as linhas** da tabela (inclui duplicadas e valores nulos).|
|**`COUNT(expr)`**|Conta apenas linhas **não nulas** na coluna especificada (`expr`).|

**Exemplo Prático**:
```SQL
-- Conta TODOS os registros do departamento 30 (mesmo com campos nulos):
SELECT COUNT(*) 
FROM scott.emp 
WHERE deptno = 30;

-- Conta apenas linhas com valores NÃO NULOS na coluna 'sal':
SELECT COUNT(sal) 
FROM scott.emp 
WHERE deptno = 30;
```
### **Observações Adicionais**

1. **Alias (`AS`)**: Melhora a legibilidade dos resultados (ex.: `"Maior Salário"`).
    
2. **Filtros (`WHERE`)**: Restringem o conjunto de dados **antes** do agrupamento.
    
3. **Precisão**: Use `ROUND()` com `AVG()` para limitar casas decimais (ex.: `ROUND(AVG(sal), 2)`).
4. 
![[Pasted image 20250402083002.png]]
 
 **Exemplo 4: Média Salarial por Departamento**
**Objetivo:** Calcular a média salarial agrupada por departamento.

```SQL
SELECT 
    deptno AS "Departamento", 
    AVG(sal) AS "Média Salarial"
FROM scott.emp
GROUP BY deptno;
```
**Saída**

|Departamento|Média Salarial|
|---|---|
|10|2916.6667|
|20|2175|
|30|1566.6667|
 **Explicação:**

1. **`GROUP BY deptno`** agrupa os registros pelo número do departamento.
2. **`AVG(sal)`** calcula a média salarial **para cada grupo**.
3. **Filtragem pré-agrupamento:** Se necessário, use `WHERE` **antes** de `GROUP BY` para restringir os dados.

 **Exemplo**:
 ```SQL
 SELECT deptno, AVG(sal)
FROM scott.emp
WHERE sal > 1000  -- Filtra antes do agrupamento
GROUP BY deptno;
```

 **Regras Importantes do `GROUP BY`**

1. **Colunas não agregadas** devem estar no `GROUP BY`.
    
    - Exemplo: Se `SELECT` inclui `deptno` e `job`, ambos devem estar em `GROUP BY`.
    
2. **Não é possível usar aliases** no `GROUP BY`.
    
    - ❌ Errado: `GROUP BY "Departamento"`
    
    - ✔ Correto: `GROUP BY deptno`
    
3. **Ordenação padrão:** Os resultados são ordenados em **ordem crescente** pelas colunas do `GROUP BY`.
    
    - Para alterar, use `ORDER BY`.
    
4. **Funções no `ORDER BY`:** É possível ordenar por uma função de grupo.
	- Exemplo:
```SQL
SELECT deptno, AVG(sal)
FROM scott.emp
GROUP BY deptno
ORDER BY AVG(sal) DESC;  -- Ordena pela média salarial (maior para menor)
```

 **Exemplo 5: Soma de Salários por Departamento e Cargo**

**Objetivo:** Calcular a folha salarial total, agrupada por departamento e cargo.

 **Consulta SQL:**
```SQL
SELECT 
    deptno AS "Departamento", 
    job AS "Cargo", 
    SUM(sal) AS "Total Salarial"
FROM emp
GROUP BY deptno, job;
```

### **Resultado:**

|Departamento|Cargo|Total Salarial|
|---|---|---|
|10|CLERK|1300|
|10|MANAGER|2450|
|30|CLERK|950|
|30|MANAGER|2850|
|30|SALESMAN|5600|

### **Explicação:**

1. **Agrupamento hierárquico:**
    
    - Primeiro, os dados são agrupados por `deptno`.
    
    - Dentro de cada departamento, são subagrupados por `job`.
    
2. **`SUM(sal)`** calcula a soma dos salários **para cada combinação de departamento e cargo**.
    
3. **Uso prático:** Ideal para relatórios de custos departamentais ou distribuição salarial por função.
    
![[Pasted image 20250402083802.png]]

---
==➡️**Dica**==

==Para melhorar a legibilidade:==
- ==Use **aliases** (`AS`) para nomes de colunas.==
- ==Formate consultas com **indentação clara** (como nos exemplos acima).==
- ==Combine `GROUP BY` com `HAVING` para filtrar **após** o agrupamento (ex.: `HAVING SUM(sal) > 2000`).==

**Cláusula HAVING em SQL**

Assim como a cláusula `WHERE` filtra linhas individuais em uma consulta SQL, a cláusula `HAVING` é utilizada para filtrar grupos de resultados após uma operação de agrupamento (`GROUP BY`).

**Funcionamento da cláusula HAVING:**

1. Primeiro, as linhas são agrupadas de acordo com a cláusula `GROUP BY`.
    
2. Em seguida, as funções de agregação (como `MAX`, `SUM`, `AVG`, etc.) são aplicadas a cada grupo.
    
3. Por fim, apenas os grupos que satisfazem a condição especificada na cláusula `HAVING` são incluídos nos resultados.
    

**Exemplo 6:** Listar os números de departamento e seus respectivos salários máximos, considerando apenas departamentos onde o salário máximo seja superior a 2.900.

```SQL
SELECT   deptno, MAX(sal)
FROM     scott.emp
GROUP BY deptno
HAVING   MAX(sal) > 2900;
```
**Resultado:**
```SQL
DEPTNO    MAX(SAL)
------    --------
10            5000
20            3000
```
**Observações:**

- A cláusula `HAVING` é sempre aplicada após o agrupamento, diferentemente do `WHERE` que filtra antes do agrupamento.
    
- É possível usar funções de agregação na condição do `HAVING`, como no exemplo acima (`MAX(sal) > 2900`).

**Subconsultas**

Uma subconsulta é uma  consulta utilizada dentro de uma instrução SQL. Pode ser utilizada dentro de instruções select, insert, delete update ou create table. Pode ser do tipo:

- **Subconsultas de uma única linha:** consultas que retornam somente uma linha da instrução SELECT interna.
- **Subconsultas de várias linhas:** consultas que retornam mais de uma linha da instrução SELECT interna.
- **Subconsultas de várias colunas:** consultas que retornam mais de uma coluna da instrução SELECT interna

**Subconsulta em Consultas**

O uso de subconsultas em Consultas é útil quando a consulta principal requer valores desconhecidos, por exemplo: Suponha que seja necessário criar uma consulta para descobrir quem recebe um salário maior que o salário de Jones, neste caso **qual é o salário de Jones?**
![[Pasted image 20250403074241.png]]
### **Solução Utilizando Subconsultas**

Para resolver esse problema, é necessário executar **duas consultas encadeadas**:

1. **Primeira consulta (subconsulta):** Identificar o salário do funcionário "Jones".
    
2. **Segunda consulta (consulta principal):** Listar todos os funcionários que recebem mais do que Jones.

```SQL
SELECT  colunas
FROM    tabela
WHERE   condição operador (
            SELECT  select_list
            FROM   tabela
            [WHERE condições_adicionais]
        );
```

 **Elementos da Estrutura:**

- **`condição`:** Comparação entre uma coluna da consulta principal e o resultado da subconsulta.
    
- **`operador`:** Pode ser `>`, `<`, `=`, `>=`, `<=`, `<>`, `IN`, `ANY`, `ALL`, etc.
    
- **`subconsulta`:** Consulta independente que retorna um valor ou conjunto de valores. Pode incluir:
    
    - Condições (`WHERE`).
        
    - Funções de agregação (`MAX`, `MIN`, `SUM`, etc.).
        
    - Múltiplas colunas (quando comparadas com `IN` ou `EXISTS`).

 **Exemplo Prático**

**Objetivo:** Encontrar funcionários que ganham mais que "Jones".

#### **Passo a Passo:**

1. **Subconsulta:** Obter o salário de Jones.

```SQL
SELECT sal
FROM emp
WHERE ename = 'JONES';
```

(Retorna, por exemplo, `2975`)_.

2. **Consulta Principal:** Filtrar salários maiores que o resultado da subconsulta.

```SQL
SELECT ename, sal
FROM emp
WHERE sal > (
    SELECT sal
    FROM emp
    WHERE ename = 'JONES'
);
```

 **Resultado Esperado:**
```SQL
ENAME      SAL
-------  -----
KING     5000
FORD     3000
SCOTT    3000
```

 **Observações Importantes**

- A subconsulta é executada **antes** da consulta principal.
    
- Se a subconsulta retornar **múltiplos valores**, use operadores como `IN` ou `ANY`.
    
- Subconsultas podem ser aninhadas em `SELECT`, `FROM`, `HAVING` e até em outras subconsultas.

- É possível colocar a subconsulta em várias cláusulas SQL:
	- cláusula WHERE
	- cláusula HAVING
	- cláusula FROM
	
- As subconsultas devem estar entre parênteses e ao lado direito do operador de comparação.

- Não utilizar uma cláusula ORDER BY a uma subconsulta.

- Utilizar operadores de uma única linha com subconsultas de uma única linha.

- Utilizar operadores de várias linhas com subconsultas de várias linhas.

 **Exemplo 4 - Subconsulta com Função de Agregação na Cláusula HAVING**

**Objetivo:**  
Listar os departamentos e seus respectivos menores salários, considerando apenas departamentos cujo menor salário seja **maior** que o menor salário do departamento 20.

#### **Consulta SQL:**
```SQL
SELECT deptno, MIN(sal) AS menor_salario
FROM scott.emp
GROUP BY deptno
HAVING MIN(sal) > (
    SELECT MIN(sal)
    FROM scott.emp
    WHERE deptno = 20
);
```

 **Passo a Passo:**

1. **Subconsulta (executada primeiro):**  
    Calcula o menor salário do departamento 20.
```SQL
SELECT MIN(sal) FROM scott.emp WHERE deptno = 20;
```
(Exemplo de retorno: `800`)_.

1. **Consulta Principal:**
    
    - Agrupa os salários por departamento (`GROUP BY deptno`).
        
    - Filtra apenas os departamentos onde o menor salário (`MIN(sal)`) é maior que o valor retornado pela subconsulta (`> 800`).
        
 **Resultado Esperado:**
 ```SQL
 DEPTNO  MENOR_SALARIO
------  -------------
10            1300
30            950

```

_(Supondo que o menor salário do depto 20 seja 800, e os deptos 10 e 30 tenham menores salários maiores que 800)_.

### **Observações Importantes:**

1. **Funções de Agregação em Subconsultas:**
    
    - Subconsultas no `HAVING` frequentemente usam funções como `MIN`, `MAX`, ou `AVG` para comparações entre grupos.
        
2. **Erro Comum:**
    
    - Usar operadores de comparação simples (`=`, `>`, `<`) quando a subconsulta pode retornar **múltiplas linhas**. Isso causa o erro:

```SQL
-- ERRO (se a subconsulta retornar mais de uma linha):
HAVING MIN(sal) > (SELECT sal FROM emp WHERE deptno = 20);
```

3. **Solução:** Use operadores como `IN`, `ANY`, ou garanta que a subconsulta retorne um único valor (como no exemplo, com `MIN(sal)`).
        
4. **Boas Práticas:**
    
    - Nomeie colunas calculadas (ex.: `AS menor_salario`) para facilitar a leitura.
        
    - Verifique se a subconsulta retorna apenas um valor quando usar operadores simples.

 **Versão Alternativa (Menor Salário MENOR que o do Depto 20):**

Se o objetivo fosse listar departamentos com menor salário **menor** que o do depto 20:

```SQL
SELECT deptno, MIN(sal) AS menor_salario
FROM scott.emp
GROUP BY deptno
HAVING MIN(sal) < (SELECT MIN(sal) FROM scott.emp WHERE deptno = 20);
```

**Resumo**

**Visões (Views)**

Uma visão (view) é uma tabela virtual que tem por base uma tabela ou outra visão (view). Uma visão (view) não tem dados próprios mas é como uma interface através da qual os dados das tabelas podem ser visualizados ou atualizados. As tabelas nas quais uma visão (view) é baseada chamam-se _tabelas-base_. A visão (view) é guardada como um comando SELECT no dicionário de dados. Podem ser utilizadas para:

- Limitar o acesso a dados;
- Ajudar na confecção de consultas complexas, por exemplo, consultar dados de uma junção de várias tabelas, sem precisar executar o comando de uma Join;
- Apresentar diferentes panoramas dos mesmos dados, contidos na mesma tabela.

```SQL

CREATE [OR REPLACE] [FORCE|NOFORCE] VIEW nome_da_view
    [(coluna1 [AS apelido1], coluna2 [AS apelido2], ...)]
AS subconsulta
[WITH CHECK OPTION [CONSTRAINT nome_da_restricao]]
[WITH READ ONLY];
```
Parâmetros e Opções:

 ➡️ OR REPLACE  - Substitui a view existente se já existir
 ➡️ FORCE  - Cria a view mesmo com dependências inválidas
 ➡️ NOFORCE  - Padrão; só cria se as tabelas referenciadas existirem
 ➡️ AS subconsulta - Consulta SQL que define os dados da view
 ➡️ WITH CHECK OPTION - Impede modificações que não atendam à condição WHERE
 ➡️ WITH READ ONLY    - Bloqueia operações DML na view


![[Pasted image 20250404081416.png]]

-----
==Há duas classificações para visão (view)s: simples e complexa:==

**Características de uma Visão (view) Simples**

- Mostra dados envolvendo apenas uma tabela;
- Não contém funções ou grupos de dados;
- É possível implementar um comando DML.

**Características de uma Visão (view) Complexa**

- Mostra dados envolvendo várias tabelas;
- Contém funções ou grupos de dados;
- Nem sempre, é possível, implementar um comando DML.

## Criação de Views em SQL

### View Simples

**Exemplo 1:** Criar uma view chamada `EMPVU10` que exiba número, nome e cargo dos funcionários do departamento 10.

```SQL
CREATE OR REPLACE VIEW empvu10
AS 
    SELECT empno, ename, job
    FROM scott.emp
    WHERE deptno = 10;
    ```
Para verificar a estrutura da view:
```SQL
DESCRIBE empvu10;
```
Resultado:
```SQL
Name      Null?    Type
--------- -------- ------------
EMPNO     NOT NULL NUMBER(4)
ENAME              VARCHAR2(10)
JOB                VARCHAR2(9)
```

**Observação:** A cláusula `OR REPLACE` permite modificar a definição da view sem necessidade de excluí-la e recriá-la, mantendo os privilégios previamente concedidos.

**Exemplo 2:** Modificar a view `empvu10` para incluir aliases nas colunas:

```SQL
CREATE OR REPLACE VIEW empvu10 (id_emp, nome, funcao)
AS 
   SELECT empno, ename, job
   FROM scott.emp
   WHERE deptno = 10;
```

### View Complexa

**Exemplo 3:** Criar uma view que mostre por departamento:

- Nome do departamento
- Menor salário
- Maior salário 
- Média salarial

```SQL
CREATE OR REPLACE VIEW dept_sum_vu (departamento, min_salario, max_salario, media_salarial)
AS 
SELECT d.dname, MIN(e.sal), MAX(e.sal), AVG(e.sal)
   FROM scott.emp e 
   JOIN scott.dept d ON e.deptno = d.deptno
   GROUP BY d.dname;
```

**Observações importantes:**

1. Em views complexas que usam funções de agregação (`MIN`, `MAX`, `AVG` etc.), é obrigatório definir aliases para as colunas calculadas.
    
2. A cláusula `GROUP BY` é essencial quando se utilizam funções agregadas com outras colunas.
    
3. A sintaxe `JOIN` explícita (com `ON`) é preferível à sintaxe implícita para maior clareza.

### Criação de View com Restrição de Integridade

 **Exemplo 4: View com WITH CHECK OPTION**

**Objetivo:** Criar uma view chamada `empvu20` contendo todos os campos da tabela `emp` para funcionários do departamento 20, com restrição para manter a integridade dos dados.

```SQL
CREATE OR REPLACE VIEW empvu20
AS 
    SELECT *
    FROM scott.emp
    WHERE deptno = 20
WITH CHECK OPTION CONSTRAINT empvu20_ck;
```

### Funcionamento da cláusula WITH CHECK OPTION:

1. **Restrição de Integridade:**
    
    - Qualquer tentativa de alterar o número do departamento (`deptno`) através desta view falhará
        
    - A view só pode exibir registros onde `deptno = 20`, portanto não permitirá modificações que violem esta condição
        
2. **Comportamento em Operações DML:**
    
    - **INSERTs:** Não podem criar registros que não atendam à condição `deptno = 20`
        
    - **UPDATEs:** Não podem modificar registros de forma que deixem de atender à condição da view
        

### Exemplo de Violação:
```SQL
UPDATE empvu20
SET deptno = 10
WHERE empno = 7788;
```
erro gerado:
```SQL
ORA-01402: view WITH CHECK OPTION where-clause violation (Constraint: EMPVU20_CK)
```

**Explicação do erro:**

1. A operação tentou alterar o departamento do funcionário 7788 para 10
    
2. Como a view só pode mostrar registros do departamento 20, esta modificação é bloqueada
    
3. O sistema retorna o erro ORA-01402 especificando qual restrição foi violada
    
4. Nenhum registro é atualizado, mantendo a integridade dos dados visíveis através desta view
    

### Vantagens desta abordagem:

- Garante que os dados modificados através da view permaneçam consistentes com sua definição
    
- Fornece um mecanismo de validação adicional no nível da view
    
- Mantém a segurança dos dados, evitando modificações inconsistentes
    
- A restrição nomeada (`empvu20_ck`) facilita a identificação do problema quando ocorrem erros
    

**Observação:** Esta restrição só afeta operações realizadas através da view. Operações diretas na tabela base não são afetadas pela cláusula WITH CHECK OPTION.

-----
---

**Exemplo 5: Criando uma visão (view) somente leitura com a cláusula WITH READ ONLY**

Para alterar a definição da view `empvu10` e torná-la somente leitura, utilize o seguinte comando:

```SQL
CREATE OR REPLACE VIEW empvu10 (employee_number, employee_name, job_title)
AS SELECT empno, ename, job
FROM scott.emp
WHERE deptno = 10
WITH READ ONLY;
```

Qualquer tentativa de inserir ou atualizar registros por meio dessa view resultará no erro do Oracle Server:  
**ORA-01733: virtual column not allowed here** (coluna virtual não permitida aqui).

---

### **Excluindo uma View**

Uma view pode ser excluída sem afetar os dados subjacentes, pois ela é apenas uma representação das tabelas base.

**Sintaxe:**
```SQL
DROP VIEW nome_da_view;
```

**Exemplo:** Excluir a view `empvu10`.

```SQL
DROP VIEW empvu10;
```

**Observações:**

- O comando `DROP VIEW` remove apenas a definição da view do banco de dados.
    
- As tabelas base permanecem intactas.
    
- Views ou aplicações que dependem da view excluída tornam-se inválidas.
    
- Apenas o criador da view ou um usuário com o privilégio `DROP ANY VIEW` pode executar essa ação.
    

---

### **Sequências no Oracle**

Uma sequência é um objeto de banco de dados que gera valores inteiros únicos, podendo ser compartilhado por múltiplos usuários. Seu principal uso é a criação de chaves primárias automáticas.

**Vantagens:**

- Elimina a necessidade de desenvolver rotinas manuais para geração de sequências.
    
- Otimiza performance e reduz código de aplicação.
    

---

### **Criando uma Sequência**

**Sintaxe:**

```SQL
CREATE SEQUENCE nome_sequencia
    [INCREMENT BY n]
    [START WITH n]
    [{MAXVALUE n | NOMAXVALUE}]
    [{MINVALUE n | NOMINVALUE}]
    [{CYCLE | NOCYCLE}]
    [{CACHE n | NOCACHE}];
```

**Parâmetros:**

- `INCREMENT BY n`: Define o intervalo de incremento (padrão: 1).
    
- `START WITH n`: Valor inicial (padrão: 1).
    
- `MAXVALUE/MINVALUE`: Limites numéricos.
    
- `CYCLE/NOCYCLE`: Permite ou não a reinicialização ao atingir o valor máximo/mínimo.
    
- `CACHE n`: Armazena valores em cache para melhor performance.

![[Pasted image 20250412071425.png]]

## **Criação e Uso de Sequências no Oracle**

**Exemplo: Criando a Sequência DEPT_DEPTNO**

Para criar uma sequência que inicia em 91, incrementa de 1 em 1, tem valor máximo 100 e mantém as configurações padrão:

```SQL
CREATE SEQUENCE dept_deptno
    INCREMENT BY 1
    START WITH 91
    MAXVALUE 100
    NOCACHE
    NOCYCLE;
```

**Explicação:**

- Essa sequência é destinada ao campo `DEPTNO` da tabela `DEPT`.
    
- **`NOCACHE`**: Desativa o armazenamento em cache para evitar lacunas na numeração.
    
- **`NOCYCLE`**: Impede a reinicialização automática ao atingir o valor máximo.
    
- Se `INCREMENT BY` for negativo, a sequência será decrescente.
    

---

## **Utilizando Sequências com NEXTVAL e CURRVAL**

As pseudocolunas `NEXTVAL` e `CURRVAL` permitem acessar valores da sequência:

- **`NEXTVAL`**: Retorna o próximo valor disponível e incrementa a sequência.
    
- **`CURRVAL`**: Retorna o valor atual (só pode ser usado após `NEXTVAL`).
    

### **Casos de Uso Válidos:**

- Em comandos `INSERT` (cláusula `VALUES` ou subconsulta).
    
- Em comandos `UPDATE` (cláusula `SET`).
    
- Em comandos `SELECT` (exceto subconsultas, `DISTINCT`, `GROUP BY`, etc.).
    

### **Restrições:**

❌ Não pode ser usado em:

- Views
    
- Consultas com `DISTINCT`, `GROUP BY`, `HAVING` ou `ORDER BY`
    
- Subconsultas em `SELECT`, `DELETE` ou `UPDATE`
    

---

 **Exemplo 1: Inserindo Dados com NEXTVAL**
Adicionar um novo departamento usando a sequência `dept_deptno`:

```SQL
INSERT INTO dept (deptno, dname, loc)
VALUES (dept_deptno.NEXTVAL, 'MARKETING', 'SAN DIEGO');
```

 **Exemplo 2: Consultando o Valor Atual (CURRVAL)**
 ```SQL
 SELECT dept_deptno.CURRVAL
FROM dual;
```

## **Alterando uma Sequência**

Para modificar uma sequência, use `ALTER SEQUENCE`. Apenas configurações futuras são afetadas.

**Sintaxe:**
```SQL 
ALTER SEQUENCE nome_sequencia
    [INCREMENT BY n]
    [{MAXVALUE n | NOMAXVALUE}]
    [{MINVALUE n | NOMINVALUE}]
    [{CYCLE | NOCYCLE}]
    [{CACHE n | NOCACHE}];
```

 **Exemplo 3: Alterando o Valor Máximo para 999999**
 ```SQL
 ALTER SEQUENCE dept_deptno
    MAXVALUE 999999;
```
**Observações:**

- Requer privilégio `ALTER` ou `ALTER ANY SEQUENCE`.
    
- Não é possível definir um `MAXVALUE` menor que o valor atual.
    
- Para reiniciar a sequência, é necessário recriá-la.
    

---

##### **Excluindo uma Sequência**

**Sintaxe:**
```SQL
DROP SEQUENCE nome_sequencia;
```

**Exemplo**
```SQL
DROP SEQUENCE dept_deptno;
```

**Permissões:**  
Apenas o proprietário ou usuários com `DROP ANY SEQUENCE` podem excluí-la.

---

## **Índices (Index) no Oracle**

 **O que é um Índice?**

Um índice é uma estrutura física que acelera consultas, mapeando valores de colunas para seus registros correspondentes. Funciona como um "atalho" para evitar varreduras completas em tabelas grandes.

 **Diferença entre Índice e Chave:**

- **Chave**: Conceito lógico (ex.: chave primária).
    
- **Índice**: Implementação física para otimização.
    

 **Quando Criar um Índice?**

✔ Colunas frequentemente usadas em `WHERE` ou junções (`JOIN`).  
✔ Tabelas grandes com consultas que retornam < 2–4% dos registros.  
✔ Colunas com alta seletividade (muitos valores distintos).

 **Quando Evitar Índices?**

✖ Tabelas com muitas operações de `INSERT`/`UPDATE` (índices reduzem performance em DML).  
✖ Colunas com poucos valores únicos (ex.: "sexo").

---

 **Exemplo: Criando um Índice**
```SQL
CREATE INDEX emp_ename_idx
ON emp(ename);
```

 **Excluindo um Índice**
```SQL
DROP INDEX emp_ename_idx;
```

**Observação:** Índices não podem ser alterados diretamente — devem ser recriados.

---
#### **Consultando o Dicionário de Dados**

 **1. Visualizando Views**
 ```SQL
SELECT view_name, text 
FROM user_views;
```

2. **Verificando Sequências**
```SQL
SELECT *
FROM user_sequences
WHERE sequence_name = 'DEPT_DEPTNO';
```

 **3. Analisando Índices**
```SQL
SELECT index_name, index_type, table_name
FROM user_indexes
WHERE index_name = 'EMP_ENAME_IDX';
```
