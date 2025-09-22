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