Escrevendo seus primeiros DAGS

O Directed Acyclic Graph (DAG) é um pipeline de dados definido em código Python. Cada DAG representa uma coleção de tarefas que você deseja executar e é organizado para mostrar as relações entre as tarefas na UI do Airflow. As propriedades matemáticas dos DAGs os tornam úteis para construir pipelines de dados:

Directed: Se multiplas tarefas existem, cada uma delas deve ter ao menos um upstream ou downstream.

Acyclic: Tarefas não podem depender de sí mesmas, isso evita lopes infinitos.

Graph: Deve ser possível visualizar em uma estrutura gráfica todas as tarefas, com relações entre tarefas definidas por nós e vértices.

Além desses requisitos, os DAGs no Airflow podem ser definidos como você precisar! Eles podem ter uma única tarefa ou milhares de tarefas organizadas de diversas maneiras.

Por exemplo, a imagem abaixo representa um DAG com três tarefas.

![[Pasted image 20250917181810.png]]

### Definindo um DAG
###### primeira forma 
```python
from airflow.sdk import dag
from pendulum import datetime

@dag(
	schedule="@daily",
	start_date=datetime(2025, 1, 1),
	description="this dags does...",
	tags=["team_a", "source_a"],
	max_consecutive_failed_dag_runs=3,
	)
	
	def my_dag():
		pass
		
my_dag()
```
###### segunda forma
```python
from airflow.sdk import task, DAG
from pendulum import datetime

with DAG(
	schedule="@daily",
	start_date=datetime(2025, 1, 1),
	description="this dags does...",
	tags=["team_a", "source_a"],
	max_consecutive_failed_dag_runs=3,
	):
		@task
		def task_a():
			print("Hello from task A!")
		
		task_a()

```

`@dag` -> inicia a DAG
`schedule` ->dita a frequência da ação
`start_date=datetime`-> a data em que a dag deve iniciar
`description` -> descrição da DAG boa para entendimento posterior, essa descrição aparece no airflow UI
`tags` -> boas para busca de dags
`max_consecutive_failed_dag_runs` -> limita o numero de tentativas da DAG após x números de falhas.

