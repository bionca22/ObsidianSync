Airflow Core Components 

**API Server** --> Fast API server serving the UI and handling task execution requests. 

 **Scheduler** --> Schedule tasks when dependencies are fulfilled

**DAG File Processor** --> Dedicated process for parsing DAGs. in the DAGs folder or in any locations that you can have, for example in a git repository.

**Metadata Database** --> A database where all metadata is stored, like Airflow instances, users that have access to your airflow instance, and so on. 

**Executor** --> Defines ==**how**== tasks are executed, ==**does not execute**== your tasks! it defines how and on which system to execute your tasks. For exemple, if you  want execute your task  in Kurbernetes cluster, than you have a kurbernetes executor. (can not be seeing)

**Queue** -- > Defines the ==**execution task order**==, and that helps to execute the tasks in the right order. (can or can not be seeing, depending on the chosen executor)

**Worker** --> Process ==**executing**== the tasks, defined by the executor.

**Trigger** --> Process running asyncio to support deferrable operadors. 

#### Questions
Question 1: 
Which of the following **best** describes the role of the scheduler in Airflow? 

 To define connections to external systems (e.g., Data Warehouses)

 To store metadata about the state of tasks

 ==To determine which tasks need to be executed and when==

 To execute the instructions defined in tasks
____

Question 2: 
Which of the following **best** describes the role of an executor in Airflow?

 To visualize the pipeline runs

 To execute the instructions of tasks

 ==To determine how and where tasks are executed==

 To store tasks ready to be executed

___

Question 3:  
Which Airflow component is in charge of executing the logic of a DAG's tasks?

 The scheduler

 ==The worker==

 The metadata database

 The executor


# How Does Airflow Run a DAG?

![[Pasted image 20250930172822.png]]


**DAG folder:** Where you put your Python files corresponding to your DAGs.

**DAG File Processor:** Parses your DAGs folder every five minutes for new DAGs. As soon it detects your new DAG file, began to serializes it into the metadata database. 

**Metadata Database:** basically store the code of your DAG in there.

**Scheduler:** The scheduler reads the metadata database, so your DAG code, and it checks if there are any tasks to run. Then the scheduler creates and schedules tasks instance objects.

**Executor:** Pushes your task instance objects into the queue, that defines how and on which system to execute tasks.


> [!danger] The Gemini tells the:
> **Mostly Correct, but often reversed in action.** The Executor is the **interface** that talks to the workers. While the Scheduler determines _what_ needs to be run and signals the Executor, the Executor's typical action (especially in the most common setups like Celery or Kubernetes) is to **pull** from the queue or **listen** for tasks to be assigned, rather than explicitly "pushing" into it.


**Queue:** To execute your tasks in the right order. 

**Workers:** Than the workers pick up the task instances form the queue, and run the python code corresponding to the tasks.

**API Server:** That serves API endpoint to handle task operations, but also the user interface. Sooner the tasks are completed, workers update the status of the tasks by going through the API server and update the status of the tasks into the metadata database.

**Whos connect to de Metadata Database?**
- Schedule 
- DAG file processor
- API server

Differently from the Airflow2 the wokers no longer communicate whit the metadata database. 

Keep in mind that it is possible to have your workers in one cluster and the rest of your Airflow componentes in a completely different network and cluster. 

## Quiz
Question 1: 
After creating your DAG in a Python file, which action do you need to take in order for Airflow to start the process of detecting and running your DAG?

 ==Put the Python file in the dags directory==

 Restart Airflow and make sure the DAG is visible on the UI

 Wait for the DAG File Processor to pick up the tasks defined in the DAG

 Launch the API server

___

Question 2:
Do the workers have direct access to the Airflow metadata database?

 Yes

 ==No==

____

Question 3:
By default, how long can it take for the Airflow DAG File Processor to detect a new DAG file in the `dags` directory?

 ==5 minutes==

 1 minute

 5 seconds

 30 seconds

