
SVM é um algoritmo de aprendizado supervisionado para classificação. A sigla significa Support Vector Machine (máquina de vetores de suporte) e seu objetivo é achar um hiperplano que separe duas classes de observações da melhor forma possível.

Primeiramente, precisamos entender o que é um hiperplano, o que é separar da melhor forma possível e, por fim, o que é um vetor de suporte.

Um hiperplano é a generalização de um plano. Quando estamos em 1 dimensão (uma variável), um hiperplano seria um ponto. Na imagem abaixo, L é um hiperplano.

![[Pasted image 20250515074027.png]]

Em duas dimensões, um hiperplano seria uma reta, e em três dimensões, seria um plano.

![[Pasted image 20250515074101.png]]

Para mais dimensões, podemos chamar somente de hiperplano.  
Agora, o que significa achar um hiperplano que separe as classes da melhor forma possível? Significa que o melhor hiperplano vai ser o que mais se distancia das duas classes de observações.

![[Pasted image 20250515074220.png]]

Entretanto, uma classe possui muitas observações. Então, quais observações serão utilizadas para achar o hiperplano que mais se distancia dos dois grupos? Utilizando os vetores de suporte.

Os vetores de suporte são os dois pontos (um de cada classe) que mais se aproximam na classe vizinha.

![[Pasted image 20250515074323.png]]

No fim das contas, o objetivo do SVM é encontrar um hiperplano até que a margem de separação entre as classes seja máxima.

![[Pasted image 20250515074403.png]]

Repare que, até agora, falamos somente de situações onde os dados estão divididos somente entre duas classes. Entretanto, o SVM funciona também para dados classificados em 3 ou mais grupos. Para isso, duas estratégias são muito utilizadas, a **`one vs one`** e a `**one vs rest`**.


A estratégia one vs one consiste em separar os dados em grupos de duas classes, dois a dois, classificar a observação em cada caso e escolher a mais votada. Por exemplo, se nossos dados são divididos entre as classes A, B e C, o SVM vai dividir entre (A; B), (A; C) e (B;C). Daí, para (A; B), o SVM classificaria como A, entre (A; C), como A, e entre (B; C) como A, e a classe escolhida seria a classe B.

![[Pasted image 20250515074938.png]]

A estratégia one vs all consiste em comparar cada classe com todas as outras classes. Por exemplo, se novamente tivéssemos as classes A, B e C, agora os grupos seriam (A; B & C), (B; A & C) e (C; B & C). Daí, o SVM classificaria a observação dentre os grupos e o mais escolhido seria a classificação final

![[Pasted image 20250515075023.png]]

Outro ponto importante é que, até então, vimos exemplos em que uma classificação linear resolveria o problema, em duas dimensões, por exemplo, o hiperplano seria uma reta. Entretanto, nem sempre os dados se comportam dessa forma.

![[Pasted image 20250515075113.png]]

Para resolver os casos não lineares, o SVM utiliza funções para transformar os dados em um espaço linear para então achar o hiperplano ideal. O espaço transformado é chamado de espaço das features.

![[Pasted image 20250515075154.png]]

**Vantagens**

- Funciona muito bem quando as classes estão muito bem separadas.
- Funciona bem quando o número de variáveis é maior que o tamanho da amostra.
- Ele guarda os vetores de suporte, o que o torna eficiente em termos de memória.

**Desvantagens**

- Pode demorar muito para ser treinado quando o conjunto de dados é muito grande.
- O SVM não fornece estimativas de probabilidade diretamente, elas são calculadas usando uma validação cruzada.
- Não funciona muito bem quando as classes estão sobrepostas.

### Código

### **Exemplo 1: SVM para Classificação Binária**

```python
# Importar bibliotecas
import numpy as np
import matplotlib.pyplot as plt
from sklearn import datasets
from sklearn.svm import SVC
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

# Criar dataset sintético (2 classes)
X, y = datasets.make_blobs(n_samples=100, centers=2, random_state=42, cluster_std=1.2)

# Dividir em treino e teste
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Treinar o SVM
model = SVC(kernel='linear')  # Kernel linear para dados linearmente separáveis
model.fit(X_train, y_train)

# Prever e calcular acurácia
y_pred = model.predict(X_test)
print(f"Acurácia: {accuracy_score(y_test, y_pred):.2f}")

# Plotar os dados e a fronteira de decisão
plt.scatter(X[:, 0], X[:, 1], c=y, cmap='viridis')
ax = plt.gca()
xlim = ax.get_xlim()
ylim = ax.get_ylim()

# Criar grid para visualizar a fronteira
xx = np.linspace(xlim[0], xlim[1], 30)
yy = np.linspace(ylim[0], ylim[1], 30)
YY, XX = np.meshgrid(yy, xx)
xy = np.vstack([XX.ravel(), YY.ravel()]).T
Z = model.decision_function(xy).reshape(XX.shape)

# Plotar fronteira e margens
ax.contour(XX, YY, Z, colors='k', levels=[-1, 0, 1], alpha=0.5, linestyles=['--', '-', '--'])
plt.title("SVM - Classificação Binária (Linear)")
plt.show()
```

**Saída**:

- Acurácia impressa no console (ex: `0.95`).
    
- Gráfico mostrando as 2 classes e a **fronteira de decisão** (linha sólida) com as **margens** (linhas tracejadas).

##### **Exemplo 2: SVM para Multiclasse (OvO e OvR)**
```python
from sklearn.multiclass import OneVsOneClassifier, OneVsRestClassifier

# Dataset sintético (3 classes)
X, y = datasets.make_blobs(n_samples=150, centers=3, random_state=42, cluster_std=1.0)

# Estratégia OvO
model_ovo = OneVsOneClassifier(SVC(kernel='linear'))
model_ovo.fit(X_train, y_train)
y_pred_ovo = model_ovo.predict(X_test)
print(f"Acurácia (OvO): {accuracy_score(y_test, y_pred_ovo):.2f}")

# Estratégia OvR
model_ovr = OneVsRestClassifier(SVC(kernel='linear'))
model_ovr.fit(X_train, y_train)
y_pred_ovr = model_ovr.predict(X_test)
print(f"Acurácia (OvR): {accuracy_score(y_test, y_pred_ovr):.2f}")

# Plotar (apenas OvO para exemplo)
plt.scatter(X[:, 0], X[:, 1], c=y, cmap='viridis')
plt.title("SVM - Multiclasse (One vs One)")
plt.show()
```

**Saída**:

- Acurácias comparando OvO e OvR.

- Gráfico com as 3 classes (cores diferentes).

### **Kernels Não-Lineares (Exemplo com RBF)**

```python
# Dataset não-linear (em formato de lua)
X, y = datasets.make_moons(n_samples=100, noise=0.1, random_state=42)
model_rbf = SVC(kernel='rbf', gamma=1)  # Kernel RBF para dados não-lineares
model_rbf.fit(X, y)

# Plotar
plt.scatter(X[:, 0], X[:, 1], c=y, cmap='viridis')
ax = plt.gca()
xlim = ax.get_xlim()
ylim = ax.get_ylim()
xx, yy = np.meshgrid(np.linspace(xlim[0], xlim[1], 100), np.linspace(ylim[0], ylim[1], 100))
Z = model_rbf.predict(np.c_[xx.ravel(), yy.ravel()]).reshape(xx.shape)
ax.contourf(xx, yy, Z, alpha=0.2, cmap='viridis')
plt.title("SVM com Kernel RBF (Não-Linear)")
plt.show()
```

**Saída**:

- Gráfico mostrando a **fronteira não-linear** aprendida pelo SVM.


### **Explicação dos Parâmetros**:

- **`kernel`**: Define o tipo de separação (linear, polinomial, RBF, etc).
    
- **`C`**: Controla a "tolerância" a erros (valores altos = menos margem, mais overfitting).
    
- **`gamma`** (para RBF): Influencia a flexibilidade da fronteira (valores altos = overfitting).