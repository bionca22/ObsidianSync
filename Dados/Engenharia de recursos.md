melhorar os dados que serão usados nos seus modelos estatísticos ou de machine learning

![[descomplica_aula_6 (1).py]]

**Técnicas de engenharia de recursos**

**Normalização** - Muito utilizado em modelos de _machine learning_ para equalizar dados de diferentes grandezas. Os valores são ajustados entre uma escala de 0 e 1. Esta alteração não muda a distribuição dos dados, porém é recomendado retirar os outliers

**LOG**

Também chamada de transformação logarítmica muito usada no processo de engenharia de recursos, podendo ser utilizada nos seguintes casos:

- Lidar com dados distorcidos para torná-lo mais próximo de uma distribuição normal.
- Diminuir a magnitude da diferença entre os dados
- Diminui os efeitos dos outliers

**Outliers**

São valores que estão muito fora da média, se distanciando dos demais dados, também chamados de dados atípicos, e uma das técnicas para poder detectar outliers é utilizando z-score.

O zscore é uma métrica que descreve em termos de desvios padrão o quanto um valor está acima ou abaixo da média de um grupo de valores.

1 desvio padrão da média quer dizer que 68% dos dados estão na média do conjunto de dados e os 32% restantes são considerados outliers sendo 16% acima da média e 16% abaixo.

2 desvios padrões da média quer dizer que 95% dos dados estão na média do conjunto de dados e os 5% restantes são considerados outliers sendo 2,5% acima da média e 2,5% abaixo.

3 desvios padrões da média quer dizer que 99,7% dos dados estão na média do conjunto de dados e os 0,3% restantes são considerados outliers sendo 0,15% acima da média e 0,15% abaixo.

**Enconding**

Quando trabalhamos com dados categóricos, em nosso dataset, estamos falando de dados como sexo, caixa postal, cor. Não podemos usar esses dados diretamente em nossos modelos, eles precisam ser convertidos em números que representem a categoria e esse processo é chamado de enconding. Podemos fazer isso no pandas de uma maneira muito fácil.

**mudar formato para DATE TIME**
```python
df_itau['data_pregao'] = pd.to_datetime(df_itau['data_pregao'], format='%Y-%m-%d')
```


Média móvel 
```python
df_itau['mm5d'] = df_itau['preco_fechamento'].rolling(5).mean()
df_itau['mm21d'] = df_itau['preco_fechamento'].rolling(21).mean()
```
Esse código cria uma média ao longo de 5 dias e outra média ao longo de 21 dias


**get dummies**

```python
emb = pd.get_dummies(df.Embarked)
```

existem 3 tipos de embarque,  1 sinaliza o tipo de embarque selecionado 
**![[Pasted image 20250506123411.png]]**

**Tópicos avançados**

Um problema em utilizar a função get_dummies é o que chamamos de multicolinearidade, isso quer dizer que em modelos de regressão linear os dados devem ser independentes entre si, e quando criamos esses dados dummies, os valores das variáveis contém uma correlação.

Por exemplo no caso do campo Sex , quando foi criado duas novas variáveis (male e female), quando male é 0 obrigatoriamente female é 1 , é isso gera o problema de multicolinearidade.

Para evitar esse problema precisamos excluir uma das colunas, e a função get_dummies já possui um parâmetro que faz isso que é o drop_first= True