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

![[Pasted image 20250923181310.png]]

![[Pasted image 20250923202257.png]]
the tasks will run sharing the same logical date
default behavior of scheduling: if the first DAG have a start date at January 1 at 10am, he will runs at that date e time right away, then after ten minutes, as defined in your scheduled interval, the second DAG runs, and it goes like that. ==The date at which your DAG runs is specified in the logical date.==

![[Pasted image 20250923182034.png]]
here it's possible put back the old default behavior whit the create_cron_data_intervals = TRUE

XCOMs

An XCom, short for "cross-communication," is a mechanism in Apache Airflow that allows tasks to **exchange small bits of data**. It's a way for a task to push a value and for a downstream task to pull that value later

![[Pasted image 20250924155525.png]]

A XCOM is identified by a key, but not only. There are meny properties that help you to identify your XCOM. For example, the DAG ID, the task ID, and so on.

==If you want to create a XCOM, then you can use the firt notation which is by calling XCOM push explicitly.==

==So here we create a XCOM with the key mynumber and the value twenty three. That value will be stored in the airflow meta database. and then another way to push a XCOM is by either using the parameter XCOM push or returning a value ,as show below, and that value will be pushed automatically into the airflow database with the key return value==

![[Pasted image 20250924161202.png]]
![[Pasted image 20250924162122.png]]

there was some ways to use XCOM.

**Size Limits**: XComs are designed for small messages. Storing large objects like entire DataFrames or large JSON files is highly discouraged. It can clog the metadata database and lead to significant performance issues. For larger data, it's better to store the data in an external location (like a data lake or database) and pass the **location** of the data using XComs.

depending on the meta database you use, you won't be able ti share up to one gigabyte of data.
![[Pasted image 20250924162349.png]]

Variables work like every other variable.

==The variables is identify by a unique key,== That's how you can fatch it in your DAX. The variable should be JSON serializable as well.

==There are multiples ways to create variables in Airflow.==
![[Pasted image 20250924164910.png]]

To create that airflow variable using environment variables, let's say you create a AIRFLOW_VAR_MYREGULARVAR, and that will be key of your variable 