
**Selecionando colunas:**
```python
df = data.Nome

df = data['Nome']

##ambas retornam a coluna "Nome"

df = data[[|'Nome', 'CPF', 'Endereço']]

##esse exemplo retorna as tres colunas separadas 
```

**Identificando o Índice**
```python
df = data.index
```

**Excluindo linhas | drop(axis=0) :**
```python
df = data.drop(['2022-10-04, 2022-10-05], axis=0)
```

**Excluindo colunas  | drop(axis=1) :**
```python
df = data.drop(['High', 'Low'], axis=1)
```

-----

**Comando Map()**
O comando maps cria uma nova coluna baseada em um dado existente adicionando um dicionário, uma series, ou funções. Nesse caso vamos criar uma coluna contendo 2.00 correspondendo a cada coluna que tiver 0:
```python
df['new_dividens'] = data['Dividends'].map({0:2.00})
```

passando uma condição para o comando map

```python
df['new_dividens'] = data['Dividends'].map({0:2.00}).where(data.inxex == '2002-10-05')
```

----

**Comando replace():**
o comando replace aceita tanto os dados aceitos pelo map quando num, float, string, regex, entre outros.

```python
df_exmp['nome_empresa'] = df_exmp['nome_empresa'].replace('Petrobras', 'Petrobras.SA')
```

----

**Procurando dados nulos | .isnull() :**
```python
df_nulo.isnull()
```
![[Pasted image 20250505112953.png]]
para facilitar pode-se descobrir quantas fazes ocorre o **TRUE** por coluna, o que significa que há um campo nulo 

```python
df_nulo.isnull().sum
```

**.sum()** soma apenas as ocorrências de **TRUE**

![[Pasted image 20250505113421.png]]

---

**Preenche campo nulo com média | .fillna() :**
```python
media = df_exmp['A'].mean()
df_exmp = df_missing['A'].fillna(media)
```

**Setar número de linhas a serem exibidas | set_option() :**
```python
pd.set_option('display.max_rows', 10)
#onde 10 é o número de linhas a ser exibido 
```

----

## Funções Matemáticas

**Agregar | selecionar um tipo de dado e somar valores referentes a cada tipo | agg()**
```python
df_prouni.groupby(['uf'])['mensalidade'].agg(['sum'])
#onde 'sum' é o tipo da agregação, agregação por soma.
```

![[Pasted image 20250505162350.png]]

agora agregar por uf e curso fazendo uma média 

```python
df_prouni.groupby(['uf', 'curso'])['mensalidade'].agg(['mean'])
```

![[Pasted image 20250505162749.png]]

é possível adicionar mais uma função para organizar os valores por ordem crescente de médias

```python
df_prouni.groupby(['uf', 'curso'])['mensalidade'].agg(['mean']).sort_values(by = ['uf', 'mean'])
```

![[Pasted image 20250505163135.png]]

----

**Função apply() :**
para utilizar função em um data frame é necessário ultilizar o apply.
```python
def duplica_bolsa(rows):
	nova_bolsa = rows * 2
	return nova_bolsa
```

```python
df['nova_bolsa'] = df['bolsa_integral_ampla'].apply(duplica_bolsa)
```

![[Pasted image 20250505164251.png]]

perceba que os campos NaN (not a number) não foram aplicados

**Agora colocaremos essa função aplicada com Lambda**

![[Pasted image 20250505164801.png]]

```python
df['nova_bolsa'] = df['bolsa_integral_ampla'].apply(lambda x : x * 2)
```

**entrega o mesmo resultado**

Agora irei criar um novo dataframe com a função lambda já aplicada

```python
df= df.assign(nova_bolsa_lambda = lambda x (x['bolsa_integral_ampla'] * 2))
```
---

### Indices

```python
frutas = ['maça', 'banana', 'abacaxi']

frutas[0]
#['maça']

frutas[0:2]
#['maça', 'banana']

frutas [1:3]
#['banana', 'abcaxi]

frutas [:2]
#['maça', 'banana']

frutas[1:]
#['banana', 'abacaxi']

frutas[-1]
#['abacaxi']
```


**Selecionando campos de um data frame | loc()**
```python
df_exempo = df.loc[ 10 : 55 , ['Nome completo', 'cpf', 'endereço']]
```

saída

| Índice | Nome completo  | CPF            | Endereço                    |
| ------ | -------------- | -------------- | --------------------------- |
| 0      | João Silva     | 111.222.333-44 | Rua A, 100 - São Paulo      |
| 1      | Maria Oliveira | 222.333.444-55 | Av. B, 200 - Rio de Janeiro |
| ...    | ...            | ...            | ...                         |
| 10     | Carlos Souza   | 333.444.555-66 | Rua C, 300 - Belo Horizonte |
| 11     | Ana Costa      | 444.555.666-77 | Av. D, 400 - Porto Alegre   |
| ...    | ...            | ...            | ...                         |
| 55     | Pedro Santos   | 999.888.777-66 | Rua Z, 500 - Curitiba       |
| 56     | Luiza Almeida  | 888.777.666-55 | Av. Y, 600 - Salvador       |
| ...    | ...            | ...            | ...                         |

**Trazer por linhas iloc()**
```python
df = df_itau.iloc[0]
#trás o conteúdo da primeira linha 
```

![[Pasted image 20250505172557.png]]

```python
df = df_itau.iloc[0:1, : ]
#trás a primeira linha com todas as colunas e inforações
```

![[Pasted image 20250505172813.png]]

```python
df = df_itau.iloc[ : , 2:4]
#trás todas as linha e duas colunas
```

![[Pasted image 20250505173045.png]]


```python
df = df_itau.iloc[1:3, 2:4]
#trás duas linhas e duas colunas
```

![[Pasted image 20250505173312.png]]

----

#### Mudando permanentemente
é necessário incluir o termo "inplace = True" se quiser tornar as mudanças permanentes, poiso data frame sempre é editado em uma cópia

reset_index()
```python
df_itau.reset_index(inplace = True, drop = True)
#inplace=Trues muda o indice permanentemente
#drop=Trues exclue o canpo que foi mudado
```

set_index()
```python
df_itau.set_index('agências', inplace = True)
#agora o número das agências são o index
```

----

## Agrupamento

Selecionar e criar tabelas apartir de um tipo de campo com pandas 
```python
pd.crosstab(df.pais, df.produto)
```

![[Pasted image 20250506083748.png]]

somando todas as linhas e colunas | margins=True

```python
pd.crosstab(df.pais, df.produto, margins=True)
```

![[Pasted image 20250506084018.png]]

mostrar se o produto tem garantia estendida 

```python
pd.crosstab(df.pais, [df.produto, df['garantia extendida']], margins=True)
```

![[Pasted image 20250506084231.png]]

crosstab e agregação

```python
pd.crosstab([df.produto], [df.pais], values=df.quantidade, aggfunc=np.sum, margins=True)
```

![[Pasted image 20250506084814.png]]

retornar a quantidade do tipo de produtos | groupby()

```python
df_tipo_tenis = df.groupby('produto')
df_tipo_tenis.nrgroups
#dá o resultado de 4 tipos produtos

df.groupby('pais').ngroups
#mostra resultados de quantos paises estão na lista

df.groupby('pais').groups
#mostra quais linhas contém informação de cada pais 

df.groupby('pais').size
#mostra a quantidade de resgistros por pais 

df.groupby('pais').get_group('Alemanha')
#mostra todos os registros ligados ao pais Alemanha

df.groupby(['pais', 'produto'])['valor_total'].sum()
#mostra o pais, o produto e a soma do valor total 
```

**Juntar campos, concatenação:**
```python
clientes['nome_completo'] = clientes.nome + ' ' + clientes.sobrenome
#cria o nome completo  em uma nova coluna
```

**agora o mesmo processo porém usando apply() e .join**

```python
clientes['nome_completo2'] = clientes[['nome', 'sobrenome']].apply(' '.join, axis=1)
#realiza exatamente a mesma tarefa 
```

![[Pasted image 20250506091506.png]]

-----

**Append()**
```python
time_junto = time1.append(time2, ignore_index=True)
#ignore_index=True vai ignorar o index que vei de cada tabela e criar um para a nova tabela
```

  
**Concat()**
```python
time_junto = pd.concat([time1, time2])
#faz exatamente como no append
```

```python
time_junto,horizontal = pd.concat([time1, time2, axis=1])
#aqui as tabelas seram adicionadas horizontalmente, uma do lado da outra. graças ao axi = 1
```

![[Pasted image 20250506103619.png]]

----

###  Meta Caracteres

Regex é uma **sequência de caracteres** que define um padrão de busca em textos.  
**Exemplo:**

- Padrão `\d{3}` busca **3 dígitos consecutivos** (como "123" em "ABC123").

### **Meta Caracteres Básicos**

São símbolos com significados especiais em regex:

|Meta Caractere|Descrição|Exemplo (Casa com...)|
|---|---|---|
|`.`|**Qualquer caractere** (exceto nova linha)|`a.c` → "aXc", "a5c"|
|`^`|**Início da string**|`^Olá` → "Olá, mundo" (mas não "Mundo, Olá")|
|`$`|**Fim da string**|`mundo$` → "Olá, mundo"|
|`*`|**Zero ou mais** ocorrências|`a*b` → "b", "aab", "aaaab"|
|`+`|**Uma ou mais** ocorrências|`a+b` → "ab", "aaab" (não "b")|
|`?`|**Zero ou uma** ocorrência|`a?b` → "b", "ab"|
|`\d`|**Dígito** (0-9)|`\d\d` → "42", "01"|
|`\w`|**Caractere alfanumérico** (a-z, A-Z, 0-9, _)|`\w+` → "A1", "abc_"|
|`\s`|**Espaço em branco** (espaço, tab, nova linha)|`a\sb` → "a b"|
|`[ ]`|**Conjunto de caracteres**|`[aeiou]` → "a", "e"|
|`[^ ]`|**Negação do conjunto**|`[^0-9]` → "a", "!" (não dígitos)|
|`\|`|**OU lógico**|`a\|b` → "a" ou "b"|
|`( )`|**Grupo de captura**|`(ab)+` → "abab"|
```python
import re

texto = "Telefone: (11) 98765-4321, Email: user@example.com"

# Busca telefone no formato (XX) XXXXX-XXXX
telefone = re.search(r'\(\d{2}\) \d{5}-\d{4}', texto)
print(telefone.group())  # Saída: (11) 98765-4321

# Extrai todos os emails
emails = re.findall(r'\w+@\w+\.\w+', texto)
print(emails)  # Saída: ['user@example.com']
```
### **Quantificadores**

Controlam quantas vezes um padrão aparece:

|Quantificador|Descrição|Exemplo|
|---|---|---|
|`{n}`|**Exatamente n vezes**|`\d{3}` → "123"|
|`{n,}`|**No mínimo n vezes**|`a{2,}` → "aa", "aaa"|
|`{n,m}`|**Entre n e m vezes**|`\d{2,4}` → "12", "1234"|
```python
# Valida data no formato DD/MM/AAAA
data_valida = re.fullmatch(r'\d{2}/\d{2}/\d{4}', "31/12/2023")
print(bool(data_valida))  # Saída: True
```

### **Caracteres de Escape**

Para buscar meta caracteres literais (como `.`, `*`), use `\`:

```python
# Busca o ponto final em uma string
ponto = re.search(r'\.', "Fim.")
print(ponto.group())  # Saída: .
```

### **Aplicações Comuns**

- **Validação de formulários** (emails, senhas, datas).
    
- **Extrair dados** de logs ou textos.
    
- **Substituições** em editores de código.
    

**Exemplo: Validar Email**
```python
email = "user@domain.com"
padrao = r'^[\w\.-]+@[\w\.-]+\.\w+$'
valido = re.match(padrao, email)
print(valido is not None)  # Saída: True
```

### ** Ferramentas Úteis**

- **Testadores online:** [Regex101](https://regex101.com/), [RegExr](https://regexr.com/).
    
- **Documentação Python:** [re — Regular expressions](https://docs.python.org/3/library/re.html).

### **Biblioteca `re` do Python** | **Expressões Regulares**

A biblioteca `re` (regular expressions) do Python é uma das ferramentas mais poderosas para manipulação de strings. Vamos explorá-la **do básico ao avançado**, com exemplos práticos e casos de uso reais.

## 🔍 **1. Introdução à Biblioteca `re`**

Principais funções:

- `re.search()`: Busca um padrão em qualquer lugar da string
    
- `re.match()`: Busca um padrão apenas no início da string
    
- `re.findall()`: Retorna todas as ocorrências do padrão
    
- `re.sub()`: Substitui ocorrências do padrão
    
- `re.split()`: Divide a string pelo padrão

exmplo
```python
texto = "123 Rua Principal"
resultado = re.match(r'\d+', texto)
print(resultado.group())  # Saída: '123'
```

### **Flags Úteis**

Modificam o comportamento da busca:

|Flag|Descrição|Exemplo|
|---|---|---|
|`re.IGNORECASE`|Ignora maiúsc/minúsc|`re.search(r'python', 'PYTHON', re.IGNORECASE)`|
|`re.MULTILINE`|^ e $ por linha|`re.findall(r'^\d+', texto, re.MULTILINE)`|
|`re.DOTALL`|. inclui \n|`re.search(r'a.b', 'a\nb', re.DOTALL)`|

##  ** Recursos Adicionais**

- [Documentação Oficial do módulo `re`](https://docs.python.org/3/library/re.html)
    
- [Regex101 - Testador Interativo](https://regex101.com/)
    
- [Regular-Expressions.info - Tutoriais](https://www.regular-expressions.info/)



# numpy

Vamos conhecer o Numpy, uma biblioteca escrita utilizando a linguagem Python com funções para se trabalhar com computação numérica, muito rápida e eficiente.

Definição NumPy é uma biblioteca para a linguagem de programação Python, que suporta o processamento de grandes, multi-dimensionais arranjos e matrizes, juntamente com uma grande coleção de funções matemáticas de alto nível para operar sobre estas matrizes. (wikipedia)

E porque usar numpy? Ele é a base do pandas, ou seja, a biblioteca pandas utiliza as funcionalidades do numpy para cálculo de array e manipulação de dados.

Com o numpy é possível:

- Criar um array multidimensional de maneira eficiente e rápida.
- Usar funções para computar operações elemento a elemento em um array ou usar operações matemáticas em arrays de forma eficiente.

No pandas existe o conceito de _dataframe_. Uma estrutura tabular de duas dimensões, no numpy temos o objeto ndarray que é a abreviação de _n-dimensional array_ que permite executar operações matemáticas em todo o bloco de forma muita rápida e eficiente.

checa o tamanho do elemento
```python
arr.size
```

**pega a primeira linha do array**
```python
arr[0,:]
```

**array com zeros e ums**
```python

np.zeros([2,2], dtype='int32')

#saida
[[0 0]
 [0 0]]

np.ones([2,2], dtype='int32')

#saida
[[1 1]
 [1 1]]
```

**ordem aleatória**
```python
np.np.random.randint(0,57, size=(3,3))
```

```python
#saída
[[12 42  8]
 [30 23 55]
 [ 5 19 33]]
```

**Reshape**
```python

import numpy as np

# Array original (1D com 8 elementos)
arr1 = np.array([1, 2, 3, 4, 5, 6, 7, 8])

# Reshape para 4 linhas x 2 colunas
arr_4x2 = arr1.reshape(4, 2)
print("4x2:\n", arr_4x2)

# Reshape para 2 linhas x 4 colunas
arr_2x4 = arr1.reshape(2, 4)
print("\n2x4:\n", arr_2x4)
````

```python
#saída
4x2:
 [[1 2]
 [3 4]
 [5 6]
 [7 8]]

2x4:
 [[1 2 3 4]
 [5 6 7 8]]
```

**transformar array em linha**
```python
arr = np.arange(8)
```

```python
#saída
[[1 2], [3 4], [5 6], [7 8]]
```


**Matriz Transposta**

```python
#matriz original
[1, 2, 3]
[4, 5, 6]

# Transpondo a matriz (3 linhas x 2 colunas)
transposta = matriz.T  # ou np.transpose(matriz)

#matriz transposta
[1, 4]
[2, 5]
[3, 6]
```

**Importar aquivo**
```python
np.genfromtxt('array.txt', delimiter=',')
```















































































