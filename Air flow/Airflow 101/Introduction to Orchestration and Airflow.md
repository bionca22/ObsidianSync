
### Streaming
Airflow is designed for **batch processing**, not for **streaming processing**. As it lacks the capability for continuous real-time data processing and immediate response to data events, whit are essential in streaming contexts.

There is a way to schedule your data pipeline continuously in Airflow. As soon as run completes the next one starts, but ir far from streaming. Streaming has deep infrastructure and data modeling implications that are not taken into account with Airflow. To sum, Airflow is not a streaming solution, however, you can still use Airflow with Kafka, which is a tool to ingest and process data in real-time and then you store the event data in the storage location where Airflow can start workflows based on those data. 

### Scalability 
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