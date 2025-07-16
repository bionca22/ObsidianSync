K-Means é um algoritmo de aprendizado não supervisionado para clusterização. Seu nome vem da forma como ele funciona, já que seu objetivo é achar centróides para cada cluster, que são a média de todas as observações pertencentes àquele cluster, fazendo isso para todos os K clusters.

- Cada cluster é representado por um **centróide** (ponto central).
- Os dados são agrupados com base na **distância** (ex: Euclidiana) até o centróide mais próximo.

**Objetivo**: Minimizar a variância _dentro_ de cada cluster.

![[Pasted image 20250517073918.png]]

Centróides nada mais são do que pontos no espaço de variáveis que temos disponíveis em nosso conjunto de dados, que estarão no centro do cluster.
### **🔹 Como Funciona?**

1. **Escolha de K**: Define-se o número de clusters (ex: *K=3*).
    
2. **Inicialização**: Os centróides são posicionados com métodos como _K-Means++_ ( Euclidiana para calcular a distância entre as observações e os centróides).
    
3. **Atribuição**: Cada ponto é associado ao centróide mais próximo.
    
4. **Atualização**: Os centróides são recalculados como a média dos pontos do cluster.
    
5. **Repetição**: Passos 3 e 4 são repetidos até a convergência (centróides não mudam mais).

![[K-means_convergence.gif]]

Existem 3 hiperparâmetros importantes do K-Means:

- n_clusters - Número de clusters que o K-Means precisa encontrar.
- max_iter - Número de iterações até encontrar o centróide ideal.
- n_init - Número de vezes que o algoritmo repete o processo inteiro de clusterização.
### **Código (Python)**
```python
from sklearn.cluster import KMeans  
import matplotlib.pyplot as plt  
from sklearn.datasets import make_blobs  

# Dados sintéticos (3 clusters)  
X, _ = make_blobs(n_samples=300, centers=3, random_state=42)  

# Criando e treinando o modelo  
kmeans = KMeans(n_clusters=3)  
kmeans.fit(X)  
labels = kmeans.labels_  

# Visualização  
plt.scatter(X[:, 0], X[:, 1], c=labels, cmap='viridis')  
plt.scatter(kmeans.cluster_centers_[:, 0], kmeans.cluster_centers_[:, 1], s=200, c='red', marker='X')  
plt.title("K-Means: 3 Clusters com Centróides (X)")  
plt.show() plt.show()
```

![[Pasted image 20250517073348.png]]

**Vantagens**

- **Simples e rápido** para datasets não muito grandes.
- **Fácil interpretação** (centróides explicam os clusters).
- **Escalável** para muitas amostras.


 **Limitações**

- **Escolha de K**: Requer definir _K_ manualmente (métodos como _Elbow Method_ ajudam).
- **Clusters esféricos**: Assume que os grupos são convexos e de tamanho similar.
- **Sensível a outliers** e inicialização aleatória.

### **💡 Dicas Práticas**

1. **Padronize os dados** (ex: `StandardScaler`) para evitar dominância de features com escalas diferentes.
2. **Use K-Means++** (default no scikit-learn) para inicialização inteligente dos centróides.
3. **Valide com métricas** como _Silhouette Score_ ou _Inertia_ (soma das distâncias quadradas
4. - Tem um funcionamento simples.
5.  Escala bem para grandes conjuntos de dados.
6. É genérico e não paramétrico.
7.  Se adapta bem para novas observações


____

# DBSCAN

DBSCAN é um algoritmo de aprendizado não supervisionado para clusterização. A sigla significa Density Based Spatial Clustering of Applications with Noise (Clusterização Espacial Baseada em Densidade de Aplicações com Ruído) e seu objetivo é encontrar vizinhanças de observações para formar os clusters. Ele faz isso determinando, para cada observação, um raio de tamanho 𝜺, que deve conter um mínimo de pontos M.

Ele, diferente do K-Means, é um ótimo algoritmo para identificar clusters de densidades, formatos e tamanhos diferentes entre si. Vamos entender passo a passo como ele funciona.

![[Pasted image 20250517080939.png]]

### **🔍 Como o DBSCAN funciona?**

O algoritmo classifica os pontos em **3 categorias**:

1. **Pontos centrais (core points)**: Pontos com pelo menos `min_samples` vizinhos dentro de um raio `eps`.
    
2. **Pontos de borda (border points)**: Pontos dentro do raio `eps` de um _core point_, mas sem vizinhos suficientes.
    
3. **Ruídos (noise points)**: Pontos que não são nem _core_ nem _border_.
    

**Passos**:

1- Escolha aleatoriamente uma observação nos dados.

2- Trace o raio de tamanho 𝜺 a partir desse ponto e classifique entre ponto central, de fronteira ou outlier, de acordo com o número mínimo M de pontos na vizinhança.

3- Se for um ponto central, ele irá determinar um cluster, e todos os pontos de fronteira farão parte desse cluster. Assim, sucessivamente, até que não haja mais nenhum ponto de fronteira.

4- Se for um ponto outlier, escolha outro ponto até que ele seja um ponto central, repetindo o passo 3.

5- Repita os dois últimos passos até não restar nenhum ponto no conjunto de dados.

![[dbscan.gif]]

**Vantagens**

- Não é necessário escolher o número de clusters.
- Funciona muito bem para identificar clusters de tamanhos e formatos diferentes.
- É ótimo para determinar ruídos como outliers.

**Desvantagens**

- Determinar o valor de 𝜺 pode ser difícil.
- Para um conjunto de dados de alta dimensão, utilizar a distância euclidiana pode ser ruim, mas achar uma distância melhor pode ser difícil.
- Não funciona bem para dados muito esparsos.

**exemplo em python**

```python
from sklearn.cluster import DBSCAN  
import matplotlib.pyplot as plt  
from sklearn.datasets import make_moons  

# Dados não lineares (formato de luas)  
X, _ = make_moons(n_samples=300, noise=0.05, random_state=42)  

# Criando e treinando o modelo  
dbscan = DBSCAN(eps=0.3, min_samples=5)  
labels = dbscan.fit_predict(X)  

# Visualização  
plt.scatter(X[:, 0], X[:, 1], c=labels, cmap="viridis")  
plt.title("DBSCAN: Clusters não lineares e outliers (ruídos)")  
plt.show() 
```


### **💡 Dicas para Usar DBSCAN**

1. **Padronize os dados** (ex: `StandardScaler`) para que `eps` faça sentido em todas as dimensões.
    
2. **Teste valores de `eps`** com um gráfico de distância (_k-distance plot_):

```python
from sklearn.neighbors import NearestNeighbors  
neighbors = NearestNeighbors(n_neighbors=5).fit(X)  
distances, _ = neighbors.kneighbors(X)  
plt.plot(np.sort(distances[:, -1]))  
plt.xlabel("Pontos")  
plt.ylabel("Distância do 5º vizinho mais próximo") plt.ylabel("Distância do 5º vizinho mais próximo")
```

![[Pasted image 20250517081648.png]]


1. - Escolha `eps` na "dobra" do gráfico (onde há um "cotovelo").
        
2. **Use `min_samples` ≥ dimensões dos dados + 1** (ex: para 2D, `min_samples=3`).

### **🌍 Aplicações do DBSCAN**

- **Segmentação de clientes** com comportamentos atípicos.
- **Detecção de fraudes** (outliers).
- **Análise de imagens** (aglomerados de pixels).