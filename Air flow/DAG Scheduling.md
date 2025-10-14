
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


