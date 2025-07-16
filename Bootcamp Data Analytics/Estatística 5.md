
#### Teste de Hipótese
![[Pasted image 20240410111018.png]]
![[Pasted image 20240410111034.png]]

nível de significância == α

![[Pasted image 20240410113203.png]]

nível descritivo ou P valor
![[Pasted image 20240410114113.png]]

Gráfico no Teste de Hipóteses
![[Pasted image 20240410114419.png]]

<h2 style="color: #F33A6A">Usando Tabela t-Student</h2>
https://www.youtube.com/watch?v=I7SLpS3fhXY

Concluindo o test
![[Pasted image 20240410121215.png]]

#### Como saber rejeitar ou aceitar uma hipóteze

##### teste Z
![[Pasted image 20240410173216.png]]
onde:
![[Pasted image 20240410170720.png]]

Se o resultado estiver fora da **Região Critica** significa aceitar **H0** e por consequência rejeitar **Ha**

![[Pasted image 20240410172358.png]]
No caso desse exemplo: A 5% de significância não há evidências de que o salário médio dos funcionários da empresa é menor que a média sugerida. 

##### Teste T
![[Pasted image 20240410173609.png]]
onde:
![[Pasted image 20240410173741.png]]
novamente se o resultado estiver fora da **Região Critica** significa aceitar **H0** e por consequência rejeitar **Ha**
![[Pasted image 20240410175057.png]]
aqui estamos aceitando H0 que significa pela significancia de 5% a média não mudou.

<h2 style="color: #F33A6A">esse assunto fica pro aqui </h2>
https://www.youtube.com/watch?v=IfiGkWIs_7Y&list=PL7xT0Gz6G0-TfV-S6WiGDvIsZds6Pv_g8&index=7


<h2 style="color: #F33A6A"> caso de uso</h2>
![[Pasted image 20240410121715.png]]
# Testes não Paramétricos

## Teste ANOVA

![[Pasted image 20240414085324.png]]

![[Pasted image 20240414085411.png]]

- As observalções são independentes 
- Osgrupos comparados apresentam a mesma variância
- Os erros são:
	- Independentes
	- provenientes de uma distribuição normal com média igual a zero e variancia constante.


![[Pasted image 20240414085715.png]]
- menor que o o nível de significancia estabelecido = Ha
 
![[Pasted image 20240414090054.png]]

para saber qual professor tem a turma com desempenho inferior teriamos que complementar o teste anova com um teste de coparação múltipla como o teste de Tuker

## Intervalos de Confiança 
![[Pasted image 20240414093842.png]]
![[Pasted image 20240414094100.png]]

## Teste KS
teste não paramêtrico para ver o quão distante a minha distribuição amostral está da minha distribuiçõ e referência ou diferênça entre uma e outra.

```
# Generando 10000 pontos de uma distribuicao normal

rvs = stats.norm.rvs(size=10000)

sns.set_style('whitegrid')

# sns.kdeplot(rvs)

sns.distplot(rvs).set_title("Exemplo: DistribuiÃ§ao Normal")

plt.show()
```

![[Pasted image 20240414101131.png]]

```
stats.kstest(rvs=rvs, cdf='norm')
```

```
KstestResult(statistic=0.005428053253586029, pvalue=0.9282715152505315, statistic_location=-0.10453613535027459, statistic_sign=1)
```
 **o P valor está acima da área de rejeição  então não podemos rejeitar a Ho** se asemelha muito a distribuição normal.

A hipótese nula do teste é de que a distribuição dos dados segue a mesma da distribuição de referencia.

Sendo assim como o pvalor é maior que 0.05, temos para um nivel de significancia de 5%, nao podemos rejeitar a hipotese nula

no caso diferênte de menor que a áre de rejeião: **hipótese nula do teste é de que a distribuição dos dados segue a mesma da distribuiçãoo de referencia.**

Sendo assim como o pvalor é menor que 0.05, temos para um nivel de significancia de 5%, rejeitamos a hipotese nula, e o dado nao segue a distribuicao normal pelo teste


### QQ PLOTS
vão sr gráficos que tem os quantis teóricos de referência com os quantis da amostra

dados da distribuição de idade do exemplo
![[Pasted image 20240414102119.png]]
dados da normal
![[Pasted image 20240414102158.png]]


![[Estatistica3_TestesHipotese.pptx (1).pdf]]


<h2 style="color: #F33A6A">Descobrindo qual o tamanho necessário da amostra</h2>


2. Calcule qual o tamanho da amostra necessária para o desenvolvimento de um teste A/B, seguindo os seguintes critérios: a. O cenário A, da base, como o inicial, que funciona hoje. b. Considere 95% de confiança de que o efeito na conversão não foi aleatório com um nível de significância de 5% (alpha = 0,05). c. Também considere 80% de certeza conseguir capturar o efeito da nova abordagem. d. O aumento para 10% de conversão.

ChatGPT

Para calcular o tamanho da amostra necessário para um teste A/B, podemos usar a fórmula para calcular o tamanho da amostra em testes de proporção, já que estamos interessados na taxa de conversão. A fórmula geral é dada por:

![[Pasted image 20240422143555.png]]

A fórmula utilizada para calcular o tamanho da amostra necessário para cada grupo em um teste A/B é a seguinte:

![[Pasted image 20240422154612.png]]

???????????

Onde:

- n é o tamanho da amostra necessário para cada grupo (A e B).
- Z é o valor crítico associado ao nível de confiança desejado (95% de confiança resultaria em Z=1,96Z=1,96).
- p é a taxa de conversão esperada no cenário A (base inicial) ou a taxa de conversão esperada na nova abordagem (para o cálculo, assumiremos 10% de conversão, ou seja, p=0.1p=0.1).
- E é o erro aceitável, ou seja, a diferença entre a taxa de conversão esperada e a taxa de conversão observada.

```
from scipy.stats import norm

# Taxa de conversão esperada (10% de conversão)
p = 0.1

# Erro aceitável (5% da taxa de conversão esperada)
E = 0.05 * p

# Valor crítico para 95% de confiança
z_critico = norm.ppf(0.975)  # Para uma confiança de 95%, usamos 0.975 para encontrar o valor crítico

# Valor crítico para 80% de poder
z_power = norm.ppf(0.80 + (1 - 0.80) / 2)  # Aqui adicionamos (1 - 0.80) / 2 para calcular o valor crítico para duas caudas

# Tamanho da amostra necessário para o grupo A
n_A = ((z_critico * np.sqrt(p * (1 - p))) / E)**2

# Tamanho da amostra necessário para o grupo B
n_B = ((z_critico * np.sqrt(p * (1 - p))) / E)**2

print("Tamanho da amostra necessário para o grupo A:", round(n_A))
print("Tamanho da amostra necessário para o grupo B:", round(n_B))

```

Vamos entender passo a passo:

1. norm.ppfnorm.ppf: Esta função é da biblioteca SciPy e é usada para calcular o valor crítico associado a uma determinada probabilidade em uma distribuição normal padrão (com média 0 e desvio padrão 1).
    
2. 0.80+(1−0.80)/20.80+(1−0.80)/2: Este é o cálculo da probabilidade acumulada para a qual queremos encontrar o valor crítico. O valor 0.800.80 representa o poder do teste desejado, que é a probabilidade de rejeitar corretamente a hipótese nula quando ela é falsa. O termo (1−0.80)/2(1−0.80)/2 é adicionado para lidar com a distribuição bicaudal. Aqui, estamos interessados em encontrar o valor crítico que deixa uma área de 80% na cauda superior da distribuição normal padrão.
    
3. norm.ppf(0.80+(1−0.80)/2)norm.ppf(0.80+(1−0.80)/2): Este é o cálculo final que usa a função `norm.ppf` para encontrar o valor crítico correspondente à probabilidade acumulada calculada na etapa anterior.
    

Em resumo, estamos calculando o valor crítico ZZ que corresponde a uma probabilidade acumulada de 0.80+(1−0.80)/20.80+(1−0.80)/2, que representa o nível de poder desejado (80%) para o teste estatístico. Este valor crítico é usado para determinar os limites do intervalo de confiança para o teste de hipótese.