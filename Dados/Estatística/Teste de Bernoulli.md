e a Distribuição Binomial

### **Teste de Bernoulli: Um experimento simples**

Um **teste de Bernoulli** é o experimento mais básico em probabilidade, que tem apenas **dois resultados possíveis**, geralmente chamados de **sucesso** e **fracasso**.

- Exemplo:
    - Jogar uma moeda: sucesso = "cara", fracasso = "coroa".
    - Fazer uma prova: sucesso = "acertar", fracasso = "errar".
- Matemática:
    - A probabilidade de sucesso é p.
    - A probabilidade de fracasso é 1−p1.
    - A variável aleatória XXX assume valores:
        - X=1 com probabilidade ,
        - X=0 com probabilidade 1−p.

### A relação entre o teste de Bernoulli e a Distribuição Binomial


>[!info] 
>- O teste de Bernoulli trata de um **único experimento binário**.
>- A binomial junta **vários experimentos Bernoulli independentes** para modelar o total de sucessos, permitindo calcular probabilidades de vários resultados possíveis (k=0,1,2,…)

 
 **Distribuição Binomial: Repetindo testes de Bernoulli**

Agora, imagine que você **repete o teste de Bernoulli várias vezes**, de forma **independente**. A **distribuição binomial** modela o **número de sucessos** (kkk) em nnn repetições do teste.

- Exemplo prático:
    - Jogar uma moeda 10 vezes e contar quantas vezes sai "cara".
    - Fazer 20 perguntas de múltipla escolha e contar quantas você acerta.

#### Como funciona:

1. Cada repetição é **um teste de Bernoulli**:
    
    - A probabilidade de sucesso em cada teste continua sendo ppp.
    - Os testes são independentes (o resultado de um teste não afeta os outros).
2. O número de sucessos (kkk) ao final de nnn testes segue a **distribuição binomial**:
    
    - A probabilidade de obter exatamente kkk sucessos é:

![[Pasted image 20241116171527.png]]
#### Resumo do conceito:

- **Um único teste de Bernoulli** (n=1) é um caso especial da binomial. Aqui, você só faz um experimento, então o resultado é diretamente 1 (sucesso) ou 0 (fracasso).
- **Vários testes de Bernoulli (n>1)**: A binomial generaliza a ideia porque conta quantos sucessos você teve ao longo de n experimentos independentes.

##### Exemplo prático para fixar

Imagine o seguinte cenário:

- Você joga uma moeda 10 vezes (n=10n = 10n=10).
- A probabilidade de sair "cara" é p=0,5p = 0,5p=0,5 (justa).

Aqui, cada lançamento é um **teste de Bernoulli**:

- Em cada lançamento, P(cara)=0,5P(\text{cara}) = 0,5P(cara)=0,5 e P(coroa)=0,5P(\text{coroa}) = 0,5P(coroa)=0,5.

Agora, queremos saber:

- **Quantas caras** saem no total após os 10 lançamentos? Isso é modelado pela **distribuição binomial** com parâmetros n=10n = 10n=10 e p=0,5p = 0,5p=0,5.

#### Calculando probabilidades:

- Qual a probabilidade de obter exatamente 5 caras (k=5k = 5k=5)? Use a fórmula da binomial: P(X=5)=(105)(0,5)5(0,5)5=0,246P(X = 5) = \binom{10}{5} (0,5)^5 (0,5)^5 = 0,246P(X=5)=(510​)(0,5)5(0,5)5=0,246

Essa ideia se aplica a qualquer número de repetições e qualquer probabilidade ppp.