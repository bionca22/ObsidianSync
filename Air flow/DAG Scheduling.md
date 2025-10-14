
When your scheduler detects that your DAG is ready to run it creates a diagram object, a instance of your DAG.

![[Pasted image 20251014084346.png]]

**Run id:** unique identifier of your tag run, it's a time stamp -> In computing, a time stamp is a sequence of characters or encoded information that identifies when a certain event occurred, giving the date and time, often down to a small fraction of a second.

By default, all of those properties are equal to the same time stamp, corresponding to the date which you tag runs.

ex: if your DAG runs on January first twenty twenty five, then the deadline level start, the logical date and the deadline interval end will have the same date.

The diagram starts with the state ->queued, then you have some taks ->running, and now the diagram has the state ->running. 
As soon as all the tasks complete, then the state of the diagram is ->success. But if the last task -> falid, your diagram will have the state ->failed.

==The diagram can have four different states-> queued, running, sucess and failed.==

==By default you can have sixteen (16) DAG runs at the same time==


**State:** Final DAG run's state.
**dag id:** Dag ID of the DAG triggered.
**logical date:** The date when the DAG runs.
**start date:** Start timestamp.
**end date:** end timestamp. 
**duration:** Time to complet the DAG Run. 
**run id:** Timestamp that uniquely.defines the DAG run.

==And you have four important properties: the run ID-> unique identifier of you diagram, the logical date, data interval start and data interval end -> that are all the same by default==.

### How DAGs are scheduled 

**start_date=** DAG's first interval
**schedule=** How often the DAG runs

most of the time you will set this parameters.

Default Behavior **(CRATE_CRON_DATA_INTERVALS=False)** 
![[Pasted image 20251014093010.png]]

but if the Default Behavior is **(CRATE_CRON_DATA_INTERVALS=True)** 
![[Pasted image 20251014093245.png]]
the tasks basically gona wait for the data interval to start, and gona have different time stamps from the  de Default Behavior set as "False".

____

The timestamp from which the Scheduler will attempt to backfill. 

**Automatic Default Time:** If you set the start_date using just the date (start_date=datetime(2025, 10, 14)), Airflow automatically assigns the time as midnight (00:00:00).

```python
from airflow.sdk import dag
from pendulum import datatime

@dag(start_date = datetime(2025, 1, 1), schedule = "@daily")
def my_dag():
```

**start_date**
 If you set your start_date as "none", then the DAG will runs only automatically, only if you trigger it from the UI, on the comand line interface.

**scheduler**
When you say that your DAG must be triggered on a specific interval of time, then you use a cron expression.

![[Pasted image 20251014095642.png]]

Because of the constitution of the month(which have different days duration), when you want set your scheduler for every 3 consecutive days you cant use a cron expression. In that case, the schedule of your DAG is relative to the previous diagram, and you can use **"duration"** whit a time delta object in order to define that your DAG should run every three days. Like this:

```python
from airflow.sdk import dag
from pendulum import datatime

@dag(start_date = datetime(2025, 1, 1), schedule = duration(days=3))
def my_dag():
```
