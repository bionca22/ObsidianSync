
### Streaming

**Streaming processing** involves analyzing data continuously and incrementally, immediately as it is generated or received. Data is treated as a constant, endless flow.

Airflow is designed for **batch processing**, not for **streaming processing**. As it lacks the capability for continuous real-time data processing and immediate response to data events, whit are essential in streaming contexts.

There is a way to schedule your data pipeline continuously in Airflow. As soon as run completes the next one starts, but ir far from streaming. 
Streaming has deep infrastructure and data modeling implications that are not taken into account with Airflow. To sum, Airflow is not a streaming solution, however, you can still use Airflow with Kafka, which is a tool to ingest and process data in real-time and then you store the event data in the storage location where Airflow can start workflows based on those data. 

### Scalability 

**Batch processing** involves collecting data over a period of time and processing the entire volume of data as a single group, or "batch," during a scheduled window.

## Questions

Question 1:
Which of the following would most likely be the root cause of errors when using Airflow for data processing? (select all that apply)

 A dedicated streaming solution (e.g., Apache Kafka) integrated with Airflow

 Number of data pipelines created

 ==Infrastructure==

 ==Resource allocation==
_____

Question 2: 
Fill in the blank:   
  
Airflow was designed to be used for _______ and not streaming.

 ==batch processing==

Question 3:  
Which of the following statements are true about Airflow? (select all that apply)

 Airflow was designed to be used as a dedicated streaming system

 ==Airflow is a scalable solution for data orchestration==

 ==Airflow can preform data processing==
 ___
  
Second use case is when you need more scalability or you need use more and more tasks, how do you make Airflow scalable? By default, Airflow is scalable, you can truly execute as many tasks as you want as long you have the correct underlying infrastructure. However, for small teams with limited resources managing and maintaining a complex infrastructure can be challenging and resource-intensive, in that case you might experience some issues to scale Airflow properly, whit one with their pros and cons.
In fact, you can see here some pretty well-known companies that run at scale, and you can see how many tasks they are ablr to run per month:

![[Pasted image 20250929185245.png]]

### Data Processing 

Airflow can process data but it is not mainly designed for that. It is designed for orchestrating and managing data workflows. That's why if you process data within Airflow, keep in mind that you can get errors if you don't have enough resources or the infrastructure to process your data.

![[Pasted image 20250929185646.png]]

![[Pasted image 20250929185939.png]]

## Airflow key terms

DAG = means A Single Data Pipeline = is for Directed Acyclic Graph

A **DAG** has an order - it can only be executed in a sequence that is **directed**, goes from beginning to end. This brings us to the term **acyclic**: a DAG has no cycles, so you always know where it starts and where it finishes. Also it's possible see as a **graph**, whit can be simple or complex, depending on your need.

Like this one:
![[Pasted image 20250930131153.png]]

Or this one:
![[Pasted image 20250930131233.png]]

Or much more comples like the following one:
![[Pasted image 20250930131407.png]]

## Task 

Task is a single unit of work in DAG, you can tink of it like a single node in the graph.

![[Pasted image 20250930134157.png]]
## Operator

Is the third key term you need to remember. An operator defines the work that the task does.

For exemple, task1 can be a **Python Operator** that is a callable object like a function that triggers a "checking data":
![[Pasted image 20250930132213.png]]

And the Task2 can be a **Bash Operator** to print "Hello, Airflow" on your on a standard output:
![[Pasted image 20250930132519.png]]

Than maybe Task3 could be a **HTTP Operator** that makes a specific http request for a url:
![[Pasted image 20250930132759.png]]

Finally Task4 could be  a **Postgres Operator** that execute a SQL request to the database:
![[Pasted image 20250930133112.png]]


Airflow has hundreds of different operators that you can use to execute different tasks. 


#### The operators can be divided in three mains categories
![[Pasted image 20250930133335.png]]
**Action Operators**: Is a operator that execute something like a postgres operator to execute a SQL request or the python operator to execute a python fuction.

**Transfer Operators**: transfer the data between a source to a destination. 

**Sensor Operators:** that allow you to wait for an event before executing the next task -- For example, you want to wait for a file or for a record in a database.


# Review

**Data Orchestration Fundamentals**

- Data Orchestration is the coordination and automation of data flow across various tools and systems to deliver quality data products and analytics
- The path to modern data orchestration solutions like Airflow had various evolutions starting with basic time-based scheduling tools (e.g., Cron, WTS), followed by proprietary software (e.g., AutoSys, Informatica), and finally older open-source solutions (e.g., Oozie, Luigi).

**Airflow for Data Orchestration**

- Airflow is an open-source tool for programmatically authoring, scheduling, and monitoring data pipelines.
- Airflow is defined by key characteristics such as pipelines-as-code with Python, built-in observability, a large open-source community, and much more!
- Airflow is used across a variety of industries, data practitioners, and use-cases.
- Airflow has key considerations to account for when using it for streaming, data processing, and when it is scaled. 

**Demystifying** **Airflow**

- Airflow can be used by single developers, single teams, and multi-teams. In each case, the way it is run is different.
- Airflow can be run using a variety of architecture types (e.g., on-premise) and systems (e.g., cloud services)
- Airflow key terms to remember:
    - DAG: A directed acyclical graph that represents a single data pipeline
    - Task: An individual unit of work in a DAG
    - Operator: The specific work that a Task performs 
- There are three main types of operators:
    - Action: Perform a specific action such as running code or a bash command
    - Transfer: Perform transfer operations that move data between two systems
    - Sensor: Wait for a specific condition to be met (e.g., waiting for a file to be present) before running the next task

# Final Quiz
Question 1:  
Examine the diagram of a data pipeline in Airflow below:   
  
![](https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fbelfihqbftwug198kgznm1s9j%2Fpublic%2F1710657347%2FGroup+982.1710657347664.png)

Each letter label represents a key term to describe the associated component of the data pipeline. Which of the following is the correct labeling of each component? 

 ==A) DAG B) Task C) Operator==

 A) Task B) DAG C) Operator

 A) Task B) Operator C) DAG

 A) Operator B) Task C) DAG
____
Question 2: 
Examine the data orchestration diagram below: 

![](https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fbelfihqbftwug198kgznm1s9j%2Fpublic%2F1710659169%2FGroup+989.1710659168733.png)

The diagram has the following labeled processes:

- A) Data ingestion of data sources
- B) Creating analytics and reporting
- C) Creating new data sets and data products
- D) Using MLFlow to productionize and manage predictive models  
      
    Which of the following **best** matches each data practitioner persona to each process in the diagram?

 A) ML Engineer B) Data Engineer C) Data Scientist D) Data Analyst

 A) Data Engineer B) Data Scientist C) Data Analyst D) ML Engineer

 ==A) Data Engineer B) Data Analyst C) Data Scientist D) ML Engineer==

 A) Data Scientist B) Data Engineer C) ML Engineer D) Data Analyst
____

Question 3:  
Which of the following scenarios would be a valid use-case for Airflow? (select all that apply)

 ==Periodic analysis on sensor data from manufacturing equipment to forecast potential failures and schedule maintenance automatically==

 As a dedicated system for processing real-time, high-volume data streams for a stock trading application

 ==A health care application that schedules email reminders for patients for their appointments==

 ==An AI chatbot that gives tips and solutions based on customer errors and actions==
 
___
Question 4:  
The benefits of using a modern data orchestration tool like Airflow is because it offers the ability to...(select all that apply)

 ==Integrate with hundreds of external systems/software==

 ==Schedule data based on events in addition to time==

 Author pipelines as configuration files

 ==Use a rich feature set with features like built-in observability==

 Store, secure and preserve large quantities of data permanently