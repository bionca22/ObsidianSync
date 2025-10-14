Escrevendo seus primeiros DAGS

O Directed Acyclic Graph (DAG) é um pipeline de dados definido em código Python. Cada DAG representa uma coleção de tarefas que você deseja executar e é organizado para mostrar as relações entre as tarefas na UI do Airflow. As propriedades matemáticas dos DAGs os tornam úteis para construir pipelines de dados:

Directed: Se multiplas tarefas existem, cada uma delas deve ter ao menos um upstream ou downstream.

Acyclic: Tarefas não podem depender de sí mesmas, isso evita loopes infinitos.

Graph: Deve ser possível visualizar em uma estrutura gráfica todas as tarefas, com relações entre tarefas definidas por nós e vértices.

**O que significa "upstream" e "downstream"?**
- **Upstream:** São as tarefas que precisam ser concluídas **antes** que uma tarefa possa ser executada. Imagine-as como os "pré-requisitos".
    
- **Downstream:** São as tarefas que dependem de uma tarefa para serem executadas. Elas são as "tarefas seguintes" no fluxo.

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

- `@dag` -> inicia a DAG
- `schedule` ->dita a frequência da ação
- `start_date=datetime`-> a data em que a dag deve iniciar
- `description` -> descrição da DAG boa para entendimento posterior, essa descrição aparece no airflow UI
- `tags` -> boas para busca de dags
- `max_consecutive_failed_dag_runs` -> limita o numero de tentativas da DAG após x números de falhas.

```python
default_args = {
    'retries': 3,
}

@dag('my_dag', start_date=datetime(2025, 1 , 1), default_args=default_args,
         description='A simple tutorial DAG', tags=['data_science'],
         schedule='@daily')
def my_dag():
    
    task_a = PythonOperator(task_id='task_a', python_callable=print_a)
    task_b = PythonOperator(task_id='task_b', python_callable=print_b)
    task_c = PythonOperator(task_id='task_c', python_callable=print_c)
    task_d = PythonOperator(task_id='task_d', python_callable=print_d)
    task_e = PythonOperator(task_id='task_e', python_callable=print_e)

    chain(task_a, [task_b, task_c], [task_d, task_e])
```

- O `PythonOperator` é um dos operadores mais comuns do Airflow. Ele permite que você execute uma função **Python** específica como uma tarefa.
- `python_callable` é a função Python que será executada, que neste caso é a função `print_a`.
- A função `chain()` é uma maneira mais concisa de definir as dependências entre as tarefas. Em vez de usar os operadores de bitwise `>>` (para dependência "downstream") ou `<<` (para dependência "upstream")

- Create a file using the **BashOperator**
- Read the file using the **PythonOperator**
# Questões

Question 1:  
What's the role of the start date?

 ==Define when the DAG starts being scheduled==

 Define the trigger interval

 Avoid running past non-triggered DAG Runs
____

Question 2: 
What happens if you don't define a start date?

 ==Nothing, it's optional==

 That raises an error

Question 3:
What's the role of tags?

 ==The allow to better organizing DAGs==

 ==They allow filtering DAGs==

 They prevent from running DAGs that do not belong to the current user
____

Question 4: 
How can you avoid assigning the dag object to every task you create?

 ==with DAG(...)==

 dag = ...

 ==@dag(..)==

 You can't. You must assign the dag object to every task
____

Question 5:
What happens when two DAGs share the same DAG id?

 The two DAGs appear on the UI

 You get an error

 ==One DAG randomly shows up on the UI==
____

Question 6:  
Does `task_a >> task_b >> task_c`

is equivalent to

`task_c << task_b << task_a`?

 ==Yes==

 No

----
## Wrap Up

Well done!  
Here are the key takeaways from this module:

1. A DAG must have a unique identifier
2. The start date is optional and set to None by default
3. The schedule interval is optional and defines the trigger frequency of the DAG
4. Defining a description, and tags to filter is strongly recommended.
5. To create a task, look at the https://registry.astronomer.io/ first.
6. A task must have a unique identifier within a DAG
7. You can specify default parameters to all tasks with default_args that expects a dictionary
8. Define dependencies with bitshift operators (>> and <<) as well as lists.
9. chain helps to define dependencies between task lists