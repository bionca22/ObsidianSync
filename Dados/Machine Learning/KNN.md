O KNN é um algoritmo **supervisionado** usado tanto para **classificação** quanto para **regressão**. Ele é um dos métodos mais simples de Machine Learning, baseado na ideia de que objetos semelhantes estão próximos uns dos outros no espaço de dados.

1. **Escolha do valor de K**:
    
    - **K** é o número de vizinhos mais próximos que o algoritmo considera para tomar uma decisão.
        
    - Exemplo: Se **K=3**, o algoritmo analisa os 3 pontos de dados mais próximos do novo dado a ser classificado.

![[Pasted image 20250514075157.png]]

### **Imagine essa situação:**

Você está em um bairro onde as casas são coloridas de **azul** ou **vermelho**, e você quer pintar **SUA CASA** com a cor "mais comum" entre seus vizinhos. Como decidir?

1. **Passo 1: Escolher quantos vizinhos perguntar**
    
    - Se você perguntar apenas **1 vizinho** (K=1), vai copiar a cor dele (arriscado, pois ele pode ser "diferente").
    
    - Se perguntar **5 vizinhos** (K=5), vê qual cor aparece mais e pinta a sua igual.
    
2. **Passo 2: Definir quem são os vizinhos mais próximos**
    
    - Você mede a distância da sua casa até as outras. Quem estiver **mais perto** (na rua ao lado) tem mais influência do que quem está longe.
    
3. **Passo 3: Contar os votos**
    
    - Se os 5 vizinhos mais próximos forem:
        
        - 3 casas **azuis**
        
        - 2 casas **vermelhas**  
	        → Sua casa será **azul**!


 **Treinamento**: O algoritmo **memoriza** todos os dados (não "aprende" nada, só guarda).
    
5. **Previsão**: Quando chega um dado novo, ele:
    
    - Calcula a distância dele para todos os outros.
    
    - Pega os **K mais próximos**.
  O KNN é um algoritmo **supervisionado** usado tanto para **classificação** quanto para **regressão**. Ele é um dos métodos mais simples de Machine Learning, baseado na ideia de que objetos semelhantes estão próximos uns dos outros no espaço de dados.

6. **Escolha do valor de K**:
    
    - **K** é o número de vizinhos mais próximos que o algoritmo considera para tomar uma decisão.
        
    - Exemplo: Se **K=3**, o algoritmo analisa os 3 pontos de dados mais próximos do novo dado a ser classificado.

![[Pasted image 20250514075157.png]]

### **Imagine essa situação:**

Você está em um bairro onde as casas são coloridas de **azul** ou **vermelho**, e você quer pintar **SUA CASA** com a cor "mais comum" entre seus vizinhos. Como decidir?

1. **Passo 1: Escolher quantos vizinhos perguntar**
    
    - Se você perguntar apenas **1 vizinho** (K=1), vai copiar a cor dele (arriscado, pois ele pode ser "diferente").
    
    - Se perguntar **5 vizinhos** (K=5), vê qual cor aparece mais e pinta a sua igual.
    
2. **Passo 2: Definir quem são os vizinhos mais próximos**
    
    - Você mede a distância da sua casa até as outras. Quem estiver **mais perto** (na rua ao lado) tem mais influência do que quem está longe.
    
3. **Passo 3: Contar os votos**
    
    - Se os 5 vizinhos mais próximos forem:
        
        - 3 casas **azuis**
        
        - 2 casas **vermelhas**  
	        → Sua casa será **azul**!

##### KNN no Machine Learning:**
 **Treinamento**: O algoritmo **memoriza** todos os dados (não "aprende" nada, só guarda).
    
 **Previsão**: Quando chega um dado novo, ele:
	-Calcula a distância dele para todos os outros.
    - Pega os **K mais próximos**.
    - "Vota" na classe mais frequente.

**Problema**: Se os dados estiverem desbalanceados (ex.: 100 Casas Vermelhas e 2 casas azuis), o KNN pode errar. Solução? Escolher **K maior** ou ajustar os dados!

![[Pasted image 20250515073536.png]]
**Distância Euclidiana**
**A1 e A2 = √( (X2-X1)² + (Y2-Y1)² )**

Portanto, o KNN vai funcionar da seguinte forma:

1. Recebe uma nova observação.
2. Calcula a distância euclidiana dos dados de treino para a nova observação.
3. Escolhe as K observações de treino mais próximas da nova observação.
4. Entre essas K observações, conta a quantidade de ocorrências em cada classe disponível nos dados.
5. Classifica o novo dado com a classe de maior ocorrência entre as K observações mais próximas.

### **Passo a Passo em Código**

#### **1. Importar bibliotecas**

```python
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import accuracy_score
from sklearn.preprocessing import StandardScaler
import matplotlib.pyplot as plt
import numpy as np
```

#### **2. Carregar os dados (dataset Iris)**

```python
iris = load_iris()
X = iris.data  # Características (comprimento/largura das pétalas e sépalas)
y = iris.target  # Rótulos (0=Setosa, 1=Versicolor, 2=Virginica)
```

#### **3. Dividir em treino e teste**

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)
```

#### **4. Normalizar os dados (importante para o KNN!)**

```python
scaler = StandardScaler()
X_train = scaler.fit_transform(X_train)
X_test = scaler.transform(X_test)
```

#### **5. Criar e treinar o modelo KNN**
```python
knn = KNeighborsClassifier(n_neighbors=3)  # K=3
knn.fit(X_train, y_train)
```

#### **6. Fazer previsões e calcular acurácia**

```python
y_pred = knn.predict(X_test)
accuracy = accuracy_score(y_test, y_pred)
print(f"Acurácia: {accuracy * 100:.2f}%")  # Exemplo: 97.78%
```

#### **7. Visualizar como o KNN classifica (em 2D para simplificar)**
```python
# Pegamos apenas 2 features para visualizar em 2D
X_2d = X[:, :2]  
y_2d = y

# Treinar um KNN só para essas 2 features
knn_2d = KNeighborsClassifier(n_neighbors=3)
knn_2d.fit(X_2d, y_2d)

# Criar um grid para visualização
x_min, x_max = X_2d[:, 0].min() - 1, X_2d[:, 0].max() + 1
y_min, y_max = X_2d[:, 1].min() - 1, X_2d[:, 1].max() + 1
xx, yy = np.meshgrid(np.arange(x_min, x_max, 0.02),
                     np.arange(y_min, y_max, 0.02))

# Prever cada ponto do grid
Z = knn_2d.predict(np.c_[xx.ravel(), yy.ravel()])
Z = Z.reshape(xx.shape)

# Plotar
plt.figure(figsize=(10, 6))
plt.contourf(xx, yy, Z, alpha=0.3, cmap='viridis')
plt.scatter(X_2d[:, 0], X_2d[:, 1], c=y_2d, cmap='viridis', edgecolor='k')
plt.xlabel('Comprimento da Sépala (cm)')
plt.ylabel('Largura da Sépala (cm)')
plt.title('Classificação KNN (K=3) no Dataset Iris')
plt.show()
```

### **Explicação do Código**

1. **Normalização**: O KNN é sensível à escala, então usamos `StandardScaler`.
    
2. **Escolha de K**: Aqui, usamos `K=3`, mas você pode testar outros valores (ex.: `K=5`, `K=7`).
    
3. **Visualização**: Reduzimos para 2D só para plotar, mas o modelo real usa todas as features.
    

---

### **Como Melhorar o Modelo?**

- **Testar diferentes valores de K**: Usar validação cruzada para escolher o melhor `K`.
    
- **Balancear os dados**: Se uma classe for dominante, o KNN pode ter viés.
    
- **Experimentar outras métricas de distância**: `metric='manhattan'` ou `metric='minkowski'`.
