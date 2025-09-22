==Provider is like a python package that has operators, hooks, and even connection types.  if you don't see a connection type on the Airflow UI, then you need to install the corresponding Airflow provider.==

Components: 
API Server -> FastAPI server serving the UI and handling task execution requests.

Scheduler -> schedule task when dependecies are fulfilled.

DAG File Processor -> Dedicated process for parsing DAGs.

Metadata Database -> A database where all metadata are stored.

Executor -> Defines **how** taskd are executed, it defines how and on which system to run tasks

Queue -> Defines the execution task order.

Worker -> Process executing the tasks, defined by the executor.

Triggerer: Process running asyncio to support deferrable operators.


![[Pasted image 20250922185347.png]]

the workers don't connect direct whit the metadata database anymore. Now you can have your Airflow instance in one cluster in a country e the workes in another country. 

Now, the Triggerer and the DAG File Processors connect with the database through an in process API server.

==The DAGs folder is not an architectural component.== 

![[Pasted image 20250922190237.png]]

==First, you will have to add your DAG file into the DAGs folder==.

When you add a new DAG file, that takes up to five minutes for Airflow to know about this new DAG file. And if you modify an existing DAG, then Airflow will take thirty seconds to know about this modification. 
==So new DAG file, five minutes. Existing DAG files, thirty seconds.==

### Defining DAG

==The scheduler uses a heuristic to define if file ias a DAG or not, and that heuristic is based on the if the words DAG os Airflow exists in a file==

![[Pasted image 20250922201843.png]]

if you define dependencies  using the task or DAG decorator, then ==make sure that you explicitly call your tasks, if you don't, you will have a error. A explicitly calling is one with the parenthesis== .

==If you try to have two list of task side by side, and then you use the right pitch shift operator, that won't work. You cannot have two list of tasks side by side==

![[Pasted image 20250922201752.png]]

linear chain, cross chain

### DAG Scheduling

state = Final DAG Run's state
dag id = DAG ID of the DAG triggered
logical date = The date when the DAG runs
start date = Start timestamp
end date = End timestamp
duration = Time to complete the DAG Run
run id = String that uniquely defines the DAG run