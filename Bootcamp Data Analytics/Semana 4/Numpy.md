![[Pasted image 20240210101349.png]]

Os arrays em NumPy usam um **tipo de dado** chamado `dtype` (tipo de dados NumPy), que é uma instância de `numpy.dtype`. O `dtype` especifica o tipo dos elementos armazenados no array. Esses tipos de dados podem ser básicos, como `int`, `float`, `bool`, etc., ou tipos de dados mais complexos, como estruturas ou registros.

Quando você cria um array NumPy, pode especificar o tipo de dados ou deixar o NumPy inferir o tipo de dados com base nos valores fornecidos. Por exemplo:

```python
import numpy as np

# Criando um array com tipo de dados float
arr_float = np.array([1.0, 2.0, 3.0])
print(arr_float.dtype)  # Saída: float64

# Criando um array com tipo de dados int
arr_int = np.array([1, 2, 3])
print(arr_int.dtype)  # Saída: int64

# Criando um array com tipo de dados bool
arr_bool = np.array([True, False, True])
print(arr_bool.dtype)  # Saída: bool
```

Se o tipo de dados não for especificado explicitamente, o NumPy tentará inferir o tipo de dados com base nos valores fornecidos.

<h2 style="color: #F33A6A">Array3D</h2>
![[Pasted image 20240210102501.png]]

Arrays de 3 e 4 dimensões são estruturas de dados multidimensionais que estendem o conceito de arrays unidimensionais (vetores) e bidimensionais (matrizes) para espaços tridimensionais e tetradimensionais, respectivamente. Eles são frequentemente usados em computação científica, processamento de imagens, análise de dados volumétricos e em muitos outros domínios onde os dados têm uma natureza multidimensional.

### Arrays de 3 Dimensões:

Um array de 3 dimensões é uma coleção de elementos organizados em uma estrutura com três eixos. Pode-se imaginar isso como uma pilha de matrizes. Por exemplo, um array de 3 dimensões pode representar uma imagem colorida, onde as dimensões são altura, largura e canais de cor (vermelho, verde e azul).

```python
import numpy as np

# Criando um array de 3 dimensões (3x3x3)
arr_3d = np.random.rand(3, 3, 3)
print(arr_3d)
```

Neste exemplo, `arr_3d` é um array de 3 dimensões com dimensões 3x3x3, ou seja, é uma matriz 3x3 onde cada elemento é, por sua vez, um array de 3 números.

### Arrays de 4 Dimensões:

Um array de 4 dimensões é uma extensão do conceito de array de 3 dimensões, onde adicionamos uma dimensão extra. Por exemplo, podemos usar um array de 4 dimensões para representar um conjunto de imagens, onde as dimensões são altura, largura, canais de cor e o número de imagens.

```python
import numpy as np

# Criando um array de 4 dimensões (2x3x3x3)
arr_4d = np.random.rand(2, 3, 3, 3)
print(arr_4d)
```

Neste exemplo, `arr_4d` é um array de 4 dimensões com dimensões 2x3x3x3, o que significa que temos um conjunto de 2 imagens, onde cada imagem tem dimensões 3x3 e cada pixel é representado por um array de 3 números (canais de cor).

Arrays de 3 e 4 dimensões oferecem uma maneira poderosa de representar e manipular dados multidimensionais em Python, especialmente com o auxílio de bibliotecas como NumPy, que fornecem suporte eficiente para operações em arrays multidimensionais.
#### No python o que seriam vetores
![[Pasted image 20240210104248.png]]
### O que seriam Matriz e Tensor
![[Pasted image 20240210104458.png]]

<h2 style="color: #F33A6A">Dimensões do array</h2>
![[Pasted image 20240210104939.png]]
**Shape** = descreve a forma do array

**Método** 
.flatten() -> achata o array se o array é 3x3 ele vira de uma dimensão só.
**ex**
![[Pasted image 20240210105759.png]]

.shape() -> diz a forma do array.
**ex**
![[Pasted image 20240210105558.png]]

.reshape() -> muda as dimenções do array.
**ex**
![[Pasted image 20240210112818.png]]

.sort()
![[Pasted image 20240211070743.png]]
o sorte acontece mantendo o agrupamento do eixo 1 que é a linha, para o sorte ser feito na coluna, devesse setar o eixo como 0
![[Pasted image 20240211070932.png]]

<h2 style="color: #F33A6A">Entendendo a estrutura de array 3D no Método</h2>
![[Pasted image 20240210114332.png]]

![[Pasted image 20240210114254.png]]
onde **C** será a quantidade de amondoados, **L** a quantidade de linhas e **Co** a quantidade de colunas.

<h2 style="color: #F33A6A">Tipos de Dados NumPy</h2>

No NumPy, os tipos de dados (dtypes) são semelhantes aos tipos de dados primitivos usados em Python, mas oferecem mais controle sobre a precisão e o tamanho dos dados. Enquanto em Python puro, temos `int`, `float` e `complex` para representar inteiros, números de ponto flutuante e números complexos, respectivamente, no NumPy, temos tipos específicos, como `int32`, `float64` e `complex128`, que garantem uma precisão fixa e um tamanho específico em bytes. Essa especificidade é crucial para garantir a consistência e eficiência das operações numéricas em grandes conjuntos de dados.

#### Atributo .dtype e tipo default
![[Pasted image 20240210131815.png]]

**String**
![[Pasted image 20240210132000.png]]

**Conversão e coerção**
![[Pasted image 20240210132339.png]]
sendo esse último possível de ver que o tipo dominante é string, em todos os casos o Numpy tentara colocar os tipos baseados nas informações que está recebedo (como receber um 4.5 e entender que se trata de um float), porém quando existir uma string no conjunto esse será o tipo de todos os dados recebidos no array.

**Hierarquia de coerção**
![[Pasted image 20240210134424.png]]
bool < int
int< float
![[giphy.webp|300]]

<h2 style="color: #F33A6A">indexação</h2>
**Quando quiser indexar uma coluna** deve-se usar o atributo **":"**
![[Pasted image 20240211070156.png]]

![[Pasted image 20240211070424.png]]
![[Pasted image 20240211070551.png]]

https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf
https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sort_values.html

#### indexação Sofisticada (fancy indexing) e Máscara (mask)
![[Pasted image 20240212185320.png]]![[Pasted image 20240212185733.png]]
![[Pasted image 20240212190111.png]]

<h2 style="color: #F33A6A">Concatenação</h2>
Concatenar = unir

**Concatenando Linhas**
```
np.concatenate((arry1, array2))
```

Concatenando colunas
```
np.concatenate((arry1, array2), axis=1)
```
axis aqui indica que o array deverá ser adicionado ao lado na forma de coluna.

![[Pasted image 20240212201810.png]]
a inequivalência leva ao erro

**Deletando com np.delete()**
![[Pasted image 20240212202239.png]]

#### Calculos com Array
tabela.sum()
soma a tabela

tabela.sum(axis=0)
soma todas as colunas

tabela.sum(axis=1)
soma todas as linhas


![[Pasted image 20240216094203.png]]

![[Pasted image 20240217064250.png]]