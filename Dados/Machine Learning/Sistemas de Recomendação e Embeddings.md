Um Sistema de recomendação é composto por um ou mais algoritmos que tem como objetivo sugerir itens relevantes para os usuários.

Usamos sistemas de recomendação sempre que temos uma grande quantidade de itens para ofertar e não sabemos quais itens cada usuário mais gostaria de ver/interagir.

Em geral, podemos dividir os algoritmos de recomendação em 3 tipos: collaborative filtering, content-based e não personalizados.

Algoritmos de collaborative filtering (filtragem colaborativa em inglês) são algoritmos que se baseiam em informações já observadas entre usuários e itens, usando esses inputs para gerar novas recomendações. Essas informações são armazenadas num formato de matriz, que chamamos matriz de preferências, ou matriz de interações usuário-item.

Portanto, o objetivo é usar as informações na matriz de preferências para estimar novas interações futuras de usuário-item ou item-item e, em alguns casos, usuário-usuário.

Algoritmos de recomendação baseados em conteúdo (content based) utilizam apenas informações dos próprios itens que estão sendo recomendados, ou dos usuários, se for o caso. Por exemplo, para recomendar títulos na Netflix, só levaríamos em conta as características de cada título, como gênero, duração, classificação etária, pessoa que dirigiu, etc.

![[Pasted image 20250519104934.png]]

Algoritmos de recomendação não personalizados vêm para suprir uma demanda de momento e, principalmente, para os usuários cold start.

Um usuário cold start é aquele que não tem nenhuma interação com os itens recomendáveis, ou possui pouca. Assim, não é possível gerar uma recomendação personalizada para essa pessoa.

Ainda, pode ser que você não queira algo parecido com o que você já consumiu, ou queira saber o que mais está bombando naquele momento.

Nesse sentido, recomendações mais genéricas são muito bem-vindas. Aqui, vale muito o negócio em que o sistema de recomendação está inserido.

----

# Alternating Least Squares (ALS)

O Alternating Least Squares (Mínimos Quadrados Alternados em inglês) é um algoritmo popular de machine learning usado principalmente em sistemas de recomendação, especialmente para fatoração de matrizes em problemas de filtragem colaborativa. ALS é um algoritmo iterativo para resolver problemas de otimização onde a função objetivo depende de dois conjuntos de variáveis que precisam ser otimizados alternadamente.

Primeiro, vamos entender o que é fatoração de matrizes para depois entender como o ALS funciona.

![[Pasted image 20250519102138.png]]

Uma fatoração de matriz é uma decomposição de uma matriz em um produto de matrizes. No caso da filtragem colaborativa, os algoritmos de fatoração de matriz funcionam decompondo a matriz de interação usuário-item no produto de duas matrizes retangulares de menor dimensionalidade.

Uma matriz pode ser vista como a matriz do usuário onde as linhas representam os usuários e as colunas são os fatores latentes. A outra matriz é a matriz de itens onde as linhas são fatores latentes e as colunas representam itens.

![[Pasted image 20250519102155.png]]

O ALS aprende a fatorar a matriz de classificação em duas matrizes: a dos usuários e a dos itens. Daí, usando as posições preenchidas da matriz de interações usuário-item, o algoritmo chega nos melhores valores para as matrizes de usuários por fatores latentes e itens por fatores latentes para que o produto delas seja o mais próximo possível do valor observado.

O resultado disso é que a matriz resultante do produto da matriz de usuário pela matriz de itens é uma matriz completamente preenchida, que vai conter as previsões das interações usuário-item que não foram observadas.

Na recomendação de itens para usuários, temos:

- Matriz de ratings R (usuários × itens)

- Queremos decompor R em duas matrizes:
    
    - U (usuários × fatores latentes)
        
    - V (itens × fatores latentes)
  Um Sistema de recomendação é composto por um ou mais algoritmos que tem como objetivo sugerir itens relevantes para os usuários.

Usamos sistemas de recomendação sempre que temos uma grande quantidade de itens para ofertar e não sabemos quais itens cada usuário mais gostaria de ver/interagir.

Em geral, podemos dividir os algoritmos de recomendação em 3 tipos: collaborative filtering, content-based e não personalizados.

Algoritmos de collaborative filtering (filtragem colaborativa em inglês) são algoritmos que se baseiam em informações já observadas entre usuários e itens, usando esses inputs para gerar novas recomendações. Essas informações são armazenadas num formato de matriz, que chamamos matriz de preferências, ou matriz de interações usuário-item.

Portanto, o objetivo é usar as informações na matriz de preferências para estimar novas interações futuras de usuário-item ou item-item e, em alguns casos, usuário-usuário.

Algoritmos de recomendação baseados em conteúdo (content based) utilizam apenas informações dos próprios itens que estão sendo recomendados, ou dos usuários, se for o caso. Por exemplo, para recomendar títulos na Netflix, só levaríamos em conta as características de cada título, como gênero, duração, classificação etária, pessoa que dirigiu, etc.

![[Pasted image 20250519104934.png]]

Algoritmos de recomendação não personalizados vêm para suprir uma demanda de momento e, principalmente, para os usuários cold start.

Um usuário cold start é aquele que não tem nenhuma interação com os itens recomendáveis, ou possui pouca. Assim, não é possível gerar uma recomendação personalizada para essa pessoa.

Ainda, pode ser que você não queira algo parecido com o que você já consumiu, ou queira saber o que mais está bombando naquele momento.

Nesse sentido, recomendações mais genéricas são muito bem-vindas. Aqui, vale muito o negócio em que o sistema de recomendação está inserido.

----

# Alternating Least Squares (ALS)

O Alternating Least Squares (Mínimos Quadrados Alternados em inglês) é um algoritmo popular de machine learning usado principalmente em sistemas de recomendação, especialmente para fatoração de matrizes em problemas de filtragem colaborativa. ALS é um algoritmo iterativo para resolver problemas de otimização onde a função objetivo depende de dois conjuntos de variáveis que precisam ser otimizados alternadamente.

Primeiro, vamos entender o que é fatoração de matrizes para depois entender como o ALS funciona.

![[Pasted image 20250519102138.png]]

Uma fatoração de matriz é uma decomposição de uma matriz em um produto de matrizes. No caso da filtragem colaborativa, os algoritmos de fatoração de matriz funcionam decompondo a matriz de interação usuário-item no produto de duas matrizes retangulares de menor dimensionalidade.

Uma matriz pode ser vista como a matriz do usuário onde as linhas representam os usuários e as colunas são os fatores latentes. A outra matriz é a matriz de itens onde as linhas são fatores latentes e as colunas representam itens.

![[Pasted image 20250519102155.png]]

O ALS aprende a fatorar a matriz de classificação em duas matrizes: a dos usuários e a dos itens. Daí, usando as posições preenchidas da matriz de interações usuário-item, o algoritmo chega nos melhores valores para as matrizes de usuários por fatores latentes e itens por fatores latentes para que o produto delas seja o mais próximo possível do valor observado.

O resultado disso é que a matriz resultante do produto da matriz de usuário pela matriz de itens é uma matriz completamente preenchida, que vai conter as previsões das interações usuário-item que não foram observadas.

Veja a matriz final:

![[Pasted image 20250519105426.png]]

**Vantagens**
- Funciona bem para matrizes usuário-item esparsas.
- É referência de mercado e funciona muito bem na prática (prêmio Netflix).
- É paralelizável.
- Funciona tanto para feedbacks explícitos quanto implícitos.

**Desvantagens**
- Não vai funcionar bem para usuários cold start.
- Pode ser difícil determinar a quantidade de fatores latentes.
- Pode ser difícil calcular feedbacks implícitos.
- Não leva em consideração as características dos usuários ou dos itens.


> Na recomendação de itens para usuários, temos:

- Matriz de ratings R (usuários × itens)

- Queremos decompor R em duas matrizes:
    
    - U (usuários × fatores latentes)
        
    - V (itens × fatores latentes)
  
Tal que R ≈ U × Vᵀ


## Formulação Matemática

**O problema de otimização é:**

minimize (sobre U e V) ∑(rᵤᵢ - uᵤ⋅vᵢᵀ)² + λ(||uᵤ||² + ||vᵢ||²)

> [!note] - **Barra dupla (∥):**
>  Quando escrita em torno de um símbolo de vetor, como `∥v∥`, representa a norma ou magnitude do vetor `v`. 
> **- Norma ou magnitude:**
A norma ou magnitude de um vetor é um valor escalar que representa o comprimento do vetor. 

Onde:
- rᵤᵢ é o rating do usuário u para o item i
- uᵤ é o vetor de fatores latentes do usuário u
- vᵢ é o vetor de fatores latentes do item i
- λ é o termo de regularização

## Como o ALS funciona

1. **Inicialização**: Comece com valores aleatórios para U e V

2. **Fase de usuários (fixar V, otimizar U)**:
    
    - Para cada usuário u, resolva:  
        uᵤ = (VᵤᵀVᵤ + λI)⁻¹ Vᵤᵀrᵤ
        
    - Onde Vᵤ são os itens avaliados por u, e rᵤ são os ratings de u

3. **Fase de itens (fixar U, otimizar V)**:
    
    - Para cada item i, resolva:  
        vᵢ = (UᵢᵀUᵢ + λI)⁻¹ Uᵢᵀrᵢ
        
    - Onde Uᵢ são os usuários que avaliaram i, e rᵢ são os ratings para i

4. **Alternar** entre as duas fases até convergência

## Implementação Básica em Python

```python
import numpy as np

def als(R, k, lambda_, max_iter=10):
    # R: matriz de ratings (usuários x itens)
    m, n = R.shape
    
    # Inicializa U e V aleatoriamente
    U = np.random.rand(m, k)
    V = np.random.rand(n, k)
    
    for _ in range(max_iter):
        # Atualizar U (fixar V)
        for u in range(m):
            # Itens avaliados pelo usuário u
            rated_items = np.where(R[u, :] != 0)[0]
            V_u = V[rated_items, :]
            R_u = R[u, rated_items]
            
            # Calcular u_u
            U[u, :] = np.linalg.solve(V_u.T @ V_u + lambda_ * np.eye(k), V_u.T @ R_u)
        
        # Atualizar V (fixar U)
        for i in range(n):
            # Usuários que avaliaram o item i
            rated_users = np.where(R[:, i] != 0)[0]
            U_i = U[rated_users, :]
            R_i = R[rated_users, i]
            
            # Calcular v_i
            V[i, :] = np.linalg.solve(U_i.T @ U_i + lambda_ * np.eye(k), U_i.T @ R_i)
    
    return U, V
```

# Embeddings

 **Representações Vetoriais de Dados**

![[Pasted image 20250519104451.png]]

Os embeddings são uma das técnicas mais poderosas em machine learning e processamento de dados atualmente. Eles transformam entidades discretas (como palavras, usuários ou produtos) em vetores contínuos de números reais que capturam relações semânticas.

Embeddings tem representações vetoriais numéricas densas de objetos e relacionamentos do mundo real. Existem várias formas de representar vetorialmente um objeto ou uma categoria. A mais utilizada delas é o One Hot Encoding, que representa categorias em vetores binários.

Entretanto, embeddings são mais interessantes, pois são capazes de trazer a nuance de similaridade entre objetos semelhantes: a representação vetorial de objetos parecidos será muito próxima no espaço vetorial.

![[Pasted image 20250519105758.png]]

O one-hot encoding é um método simples de representar variáveis categóricas. É um algoritmo não supervisionado que faz um de-para de uma categoria para um vetor, onde os valores possíveis são 0 ou 1.

Assim, é criado um vetor para cada categoria, do tamanho do número de categorias, em que as posições são iguais a 0 se a observação não possuir aquela categoria, e 1 se possuir.

A grande desvantagem desse método é que categorias que possuem similaridade na vida real, não terão nenhum tipo de similaridade no vetor de espaços, pois todas as categorias estão equidistantes.

![[Pasted image 20250519110848.png]]

Por outro lado, um embedding captura parte dos objetos, como textos, colocando textos semelhantes próximos uns dos outros no espaço embedding. Um embedding pode ser aprendido e reutilizado entre os modelos.

![[Pasted image 20250519111016.png]]

#### Tipos Comuns de Embeddings

##### 1. Word Embeddings (para NLP)

- **Word2Vec**: Modelo predictivo (CBOW e Skip-gram)
- **GloVe**: Baseado em co-ocorrência global
- **FastText**: Considera subword information

#### Propriedades para Embeddings e Boas Práticas 

1. **Similaridade**: Entidades similares devem ter embeddings próximos

2. **Analogias**: Operações vetoriais devem refletir relações lógicas

3. **Generalização**: Devem ser úteis para múltiplas tarefas

4. **Eficiência**: Representação compacta mas informativa

5. **Dimensionalidade**: Comece com 50-300 dimensões

6. **Quantidade de dados**: Quanto mais, melhores os embeddings

7. **Pré-treinados**: Use embeddings pré-treinados quando possível

8. **Fine-tuning**: Ajuste para seu domínio específico

9. **Visualização**: Sempre visualize para entender o que foi aprendido


#### Como são Aprendidos?

O processo geral envolve:

1. Definir uma tarefa proxy (ex: prever palavras vizinhas)

2. Criar uma arquitetura que mapeie entidades para vetores

3. Ajustar os vetores para desempenho na tarefa proxy

4. Extrair os embeddings como subproduto do treinamento

#### Aplicações dos Embeddings

1. **Busca de informação**: Encontrar documentos similares

2. **Sistemas de recomendação**: Usuários e produtos como vetores

3. **Classificação de texto**: Usar word embeddings como features

4. **Detecção de anomalias**: Itens com embeddings atípicos

5. **Visualização de dados**: Redução para 2D/3D com t-SNE ou UMAP

## Exemplo Prático: Word Embeddings com Word2Vec

```python
from gensim.models import Word2Vec

# Dados de exemplo (sentences tokenizadas)
sentences = [
    ["o", "gato", "está", "sobre", "o", "tapete"],
    ["o", "cachorro", "está", "do lado", "da", "cama"],
    ["o", "gato", "está", "dormindo"]
]

# Treinando o modelo
model = Word2Vec(sentences, vector_size=100, window=5, min_count=1, workers=4)

# Obtendo embeddings
gato_embedding = model.wv["gato"]
print(f"Embedding para 'gato': {gato_embedding[:5]}...")  # Mostrando apenas os 5 primeiros valores

# Encontrando palavras similares
similares = model.wv.most_similar("gato", topn=3)
print(f"Palavras similares a 'gato': {similares}")
```

## Operações com Embeddings

Você pode fazer operações interessantes:

```python
# Analogia clássica: rei - homem + mulher ≈ rainha
result = model.wv.most_similar(positive=['rei', 'mulher'], negative=['homem'], topn=1)
print(result)

# Similaridade entre vetores
similarity = model.wv.similarity('gato', 'cachorro')
print(f"Similaridade entre gato e cachorro: {similarity:.2f}")
```

#### Desafios

1. **Vocabulário fora do conjunto (OOV)**: Como lidar com novas palavras?

2. **Bias**: Embeddings podem capturar vieses dos dados

3. **Interpretabilidade**: Difícil entender o que cada dimensão representa

---

**Word2Vec**

Word2vec gera embeddings de palavras. As palavras são codificadas em vetores one-hot e alimentadas em uma camada oculta de uma rede neural, que gera pesos ocultos. Esses pesos ocultos são usados para prever outras palavras próximas.

Embora esses pesos ocultos sejam usados para treinamento, o word2vec não os usará para a tarefa em que foi treinado. Em vez disso, os pesos ocultos são retornados como os próprios embeddings.

![[Pasted image 20250519112248.png]]

As palavras encontradas em contextos semelhantes terão embeddings parecidos. Além disso, os embeddings podem ser usados para formar analogias. Por exemplo, o vetor do rei ao homem é muito semelhante ao da rainha para a mulher.

Um problema com Word2Vec é que palavras únicas têm um mapeamento de vetor. Isso significa que todos os usos semânticos de uma palavra são combinados em uma representação.

Por exemplo, a palavra “jogar” em “vou me jogar nesse curso” e “eu vou jogar bola” terá o mesmo embedding, sem a capacidade de distinguir o contexto.

Além disso, é um algoritmo custoso, que precisa de bastante recurso para ser treinado para grandes conjuntos de dados.

**Tópicos avançados**

Existem vários algoritmos de recomendação já implementados em Python e disponíveis em bibliotecas open source para serem utilizados. O mais importante é entender qual tipo de estratégia de recomendação é a melhor para ser utilizada em cada caso. Deixo duas referências de recomendação do mercado, o case da Netflix e o da Amazon.

[https://research.netflix.com/research-area/recommendations](https://research.netflix.com/research-area/recommendations) 

[https://assets.amazon.science/76/9e/7eac89c14a838746e91dde0a5e9f/two-decades-of-recommender-systems-at-amazon.pdf](https://assets.amazon.science/76/9e/7eac89c14a838746e91dde0a5e9f/two-decades-of-recommender-systems-at-amazon.pdf) 

Além disso, quando pensamos em embeddings, temos diversos algoritmos para treinar e testar com nossos dados de texto. Entre eles, vale mencionar o **GloVe** e o **Doc2Vec,** que podem ser boas alternativas para o Word2Vec. Seguem os links abaixo:

[https://medium.com/@mishra.thedeepak/doc2vec-simple-implementation-example-df2afbbfbad5](https://medium.com/@mishra.thedeepak/doc2vec-simple-implementation-example-df2afbbfbad5) 

[https://towardsdatascience.com/a-comprehensive-python-implementation-of-glove-c94257c2813d](https://towardsdatascience.com/a-comprehensive-python-implementation-of-glove-c94257c2813d)