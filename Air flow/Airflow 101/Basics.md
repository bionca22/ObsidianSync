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

## DAG Setup

![[Pasted image 20251001151345.png]]

always when you use a DAG decorator you will need define a function corresponding to your DAG, in this case My_dag(). 

My DAG will be the unique identifier of your DAG. Than within that function corresponding to your DAG you will define the task, and here, two tasks: 

**Task a** is using the python operator to run code.
**Task b** is using the bash operator to run bash commands.

# Questions

Examine the following code:  
  
`from airflow.sdk import dag   from airflow.providers.standard.operators.python import PythonOperator`

In your own words, what does this code do?

==Your response:import the DAG and the python operator==

___

Question 2:
In which part of a DAG file would you specify how often you want to trigger the DAG?

 In the import statements

 ==In the DAG object definition==

 In the DAG's dependencies

 In the DAG's tasks
 ___

#### Task dependencys 

![[Pasted image 20251001152058.png]]

between **task a** and **task b** you see a shift operator, in that way it means that **task a** runs first and then **task b**, witch means that task a is a **upstream** and task b is **downstream**.

But you can also use the left bit shift operator, and in this case the first task becomes downstream and de second one becomes the upstream, just the oposite 

![[Pasted image 20251001152349.png]]

## Review

**Airflow Architecture**

- Airflow has seven main components:

- The API server for serving the Airflow UI and providing endpoints for Workers to communicate with the Airflow DB.
- The metadata database is used to store all metadata (e.g., users, tasks) related to your Airflow instance.
- The scheduler for monitoring and scheduling your pipelines.
- The executor defines how and on which system tasks are executed.
- The DAG File Processor that retrieves and parses DAG files.
- The queue for holding tasks that are ready to be executed.
- The worker(s) for executing instructions defined in a task.  
      
    

- Airflow runs DAGs in six different steps:

- The DAG File Processor constantly scans the DAGs directory for new files. The default time is every 5 minutes.
- After the DAG File Processor detects a new DAG, the DAG is processed and serialized into the metadata database.
- The scheduler checks for DAGs that are ready to run in the metadata database. The default time is every 5 seconds.
- Once a DAG is ready to run, its tasks are put into the executor's queue.
- Once a worker is available, it will retrieve a task to execute from the queue.
- The worker will then execute the task.

**DAG Components**

- A DAG has four core parts:

- The import statements, where the specific operators or classes that are needed for the DAG are defined.
- The DAG definition, where the DAG object is called and where specific properties, such as its name or how often you want to run it, are defined.
- The DAG body, where tasks are defined with the specific operators they will run.
- The dependencies, where the order of execution of tasks is defined using the right bitshift operator (>>) and the left bitshift operator (<<).  
      
    

- A DAG’s task can be either upstream or downstream to another task.


## Questions
Which of the following Airflow components does the metadata database communicate with? 

 The queue

 ==The API server==

 ==The scheduler==

 The worker(s)

___

Question 2:
Examine the image below of a DAG file:   
  
![](https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fbelfihqbftwug198kgznm1s9j%2Fpublic%2F1711751183%2FGroup+1037.1711751183238.png)  
  
Which of the following represents the correct association of each letter to its respective file component description? 

 A. Import Statements B. Tasks (Operators) C. Dependencies D. DAG Object

 A. Import Statements B. Tasks (Operators) C. DAG Object D. Dependencies

 ==A. Import Statements B. DAG Object C. Tasks (Operators) D. Dependencies==

 A. Import Statements B. DAG Object C. Dependencies D. Tasks (Operators)

___

Question 3: 
Assume a DAG has 3 tasks: `**task_extract**`, `**task_transform**`, and `**task_load**`.  
  
Which of the following represents the dependencies in a DAG that needs to meet the following conditions:

- `task_transform` is downstream of `task_extract`.
- `task_load` is downstream of `task_transform`.

 task_extract << task_load << task_transform

 ==task_extract >> task_transform >> task_load==

 task_extract >> task_load >> task_transform