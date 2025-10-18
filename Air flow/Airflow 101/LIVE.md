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
#### Best Practices for Using Environment Variables

- **Prefix with `AIRFLOW__`:** To be recognized by Airflow, your environment variables must follow the `AIRFLOW__<SECTION>__<KEY>` format. The `__` acts as a separator.
    
    - **Example:** `AIRFLOW__CORE__DAGS_FOLDER` sets the `dags_folder` option in the `[core]` section.

The correct way to create an Airflow variable using an environment variable is to prefix the environment variable with **`AIRFLOW_VAR_`**. Airflow's scheduler automatically reads any environment variable that starts with this prefix and converts it into a key-value pair in its database.

- The actual key of the Airflow variable would be **`MYREGULARVAR`** (the part after the `AIRFLOW_VAR_` prefix).
    
- The **value** of the environment variable (e.g., `export AIRFLOW_VAR_MYREGULARVAR="my_value"`) becomes the value of your Airflow variable.

![[Pasted image 20250924182522.png]]
### Connections

Connection will have the snowflake type with all the parameters that your connection needs to connect to snowflake.

==If you don't see the connection type that  you need when you create a connection, that means you have to install the corresponding Airflow provider.==

![[Pasted image 20250924183430.png]]

==every time you want to use the environment variables to create connections in airflow you will need use AIRFLOW_CONN_idname of your connection, then the string corresponding to your connection with the login, the password, and so on.== (pelo menos duas questões sobre isso)

If you want to truly secure your connections, you should use a secret backend. And the you have the airflow CLI if you want to creat connections

### Sensors

![[Pasted image 20250924184542.png]]

==a Sensor waits for a event and you have many sensors==

A Sensor is typically a typr os operator that checks is a condition is met at specific interval. So for example you havethe file sensor to wait for a file at specific interval of time. As soon the condition is met, will succeed and  then will move to the next downstream tasks.

![[Pasted image 20250929165217.png]]

poke interval e poke mode, the poke mode is the default mode. Your sensor will check every five minutes, for exemple. In the default mode your sensor takes a worker slot, end any time a worker is taken it's occupied until the task finishes. By default you have a twenty eight worker slots.

YOu can use another mode which is the reschedule mode, and the reschedule mode will free your worker slot while the sensor is waiting. So you can execute all the tasks while the sensor is waiting.

Just keep in mind that if you expect that what you are waiting for will take longer than five minutes, for example you should definitely use the reschedule mode. And if you expect that it is that it will be shorter than five minutes, then you should use poke mode. Becouse you definitely don't want to have enough worker slots to execute other tasks. And that's basically, this is little bit more advanced, but this is where deferrable operators are useful. 

==For the certification, remember, lower shorter than five minutes, depoke mode. Longer than five minutes, reschedule.== 

==The start date is not required anymore. You don't have to specify the start date in your DAGs. Now the start date has a default value and that default value is null.==

==You will have some questions about diagrams. If you want to initialize the Airflow meta database manually, you will have to run the command airflow db migrate== 

And that means Airflow was scheduling all the non paired diagrams between the start date or the last time your DAG was triggered an the current date. Now by default the catch up is set to false.

==The DAG folder is not an architectural component.==

1. Which of the following best describes the role of the Airflow scheduler?
		A. To execute tasks
		B. to both trigger worflows and submit tasks to the executor to run 
		C. To define how tasks are executed on which system 
		D. To notify when task run, retry, or fail.
	(resposta correta "B").  (''C'' is the definition of **executor**, he define how tasks are executed and on which system, and then the workers execute the tasks. So ''A'' is the definition of the workers)

2. A DAGs runs daily with a start_date 2025/01/01 00:00. When will the 3rd Dag run be triggered?
		A. 2025/01/01 00:00
		B. 2025/01/02 00:00
		C. 2025/01/03 00:00
		D. 2025/01/04 00:00
		(resposta correta "B"). (no antigo Airfloe seria "D") 

![[Pasted image 20250929172041.png]]
(resposta correta C). ( two list of tasks side by side that does not work you have to use chain in that case.)

3. You made a mistake and two DAGs have the same DAG id. What do you expect to se?
		A. An error on the Airflow UI
		B. The DAG having the earling start_date
		C. The two DAGs side by side
		D. One DAG randomly picked by Airflow
(resposta correta "D"). (Airflow can maybe trigger an erro, so cabe recurso in this mother flocker).

4. Can you have two Xcoms with the same id (name)?
	A. yes, a XCOM is defined by its id, task_id and dag_id
	B. yes, a XCOM is defined by its id and dag_id
	C. yes, but Airflow will randomly return one or the other in your DAGs 
	D. No, Airflow thows an error on the user interface.
(resposta correta "A"). (A XCOM has more than just an ID to be identified with. It has more propertis, even the date at which that XCOM was created, and so on).



![[Pasted image 20250929173852.png]]

![[Pasted image 20250929180432.png]]

Implementation code 
![[Pasted image 20250929180626.png]]
![[Pasted image 20250929180911.png]]

==Be familiar with the task flow API, with the task decorator and the tag decorator, becouse most of the code that you will see in the exam will be based on the taskflow API.==