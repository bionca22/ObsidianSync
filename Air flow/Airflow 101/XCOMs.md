![[Pasted image 20251014132420.png]]

let's say you wanna grab information from API whit 'A' e pass to 'B', XCOM function like a box that stores that information in the metadata database so 'B' can pull.

So how can task B knows which XCOM has his information? XCOM is identified in many ways, one off them is the **key**: it has always a key and it don't need to be unique because XCOM has more ways to be called. 

In addition to the key you have a **run ID**, the **DAG id**, or the **task id** where the XCOM was created, can be use to identify. Most of the time you will only identify the key and Task ID.

 To share it out between your tasks you will use the XCOM mechanism. Basically, you push the value from the task and that creates a XCOM with the value that you want to share in it.

### Using 
```python
from airflow.sdk import dag, task, Context

@dag
def xcom_dag():
	@task
	def task_a(**context: Context):
		val = 42
		context['ti'].xcom_push(key='my_key', value=val)
		
	@task
	def task_b(**context: Context:)
		val = context['ti'].xcom_pull(task_ids='task_a', key='my_key')
		
		print(val)
	task_a() >> task_b()
	
xcom_dag()
```

easier way
```python
@dag
def xcom_dag():
	
	@task
	def task_a():
		val = 42
		return val
		
	@task
	def task_b(ti):
		
	val = task_a(val: int):
		print(val)
	
xcom_dag()	
```

another way:
```python
@dag
def xcom_dag():
	
	@task
	def task_a(ti):
		val = 42
		ti.xcom_push(key='my_key', value=val)
		
	@task
	def task_b(ti):
		print(val)
		
	val = task_a()
	task_b(val)
	
xcom_dag()	
```

multiple variables in multiple tasks:
```python
@dag
def xcom_dag():
	
	@task
	def task_a(ti):
		val = 42
		ti.xcom_push(key='my_key', value=val)
		
	@task
	def task_c(ti):
		val = 46
		ti.xcom_push(key='my_key', value=val)	
		
	@task
	def task_b(ti):
		vals = ti.xcom_pull(task_ids=["task_a","task_c"], key="my_key")
		print(vals)
		
	task_a() >> task_c() >>	task_b()
	
xcom_dag()
```

multiple variables in one task:
```python
@dag
def xcom_dag():
	
	@task
	def task_a(ti):
		val = {
			"val_1": 42,
			"val_2": 46,
		}
		ti.xcom_push(key='my_key', value=val)
		
	@task
	def task_b(ti):
		vals = ti.xcom_pull(task_ids="task_a", key="my_key")
		print(vals)
		
	task_a() >>	task_b()
	
xcom_dag()
```