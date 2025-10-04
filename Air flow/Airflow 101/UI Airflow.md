One of the main features of Airflow is its [user interface (UI)](https://airflow.apache.org/docs/apache-airflow/stable/ui.html), which provides insights into your DAGs and DAG runs. The UI is essential for understanding, monitoring, and troubleshooting your pipelines.

### Overview of your DAGs and Task instances

Links that can help you:

- [https://docs.astronomer.io/learn/airflow-ui#dags](https://docs.astronomer.io/learn/airflow-ui#dags)

The main pages of Airflow give some importante metrics regarding you Airflow instances but also diagrams and task instances.

Here we can see the **health** status  of different airflow components and some frames of the DAGs status:
![[Pasted image 20251004144638.png]]

And by the **History** you can set the date you wanna explore and get metrics regarding diagrams and task instances:
![[Pasted image 20251004145134.png]]
Because you tasks can have many different states they are not listed here, but if you have tasks that are in the running state or in the failed state, they can been seen through the panel.

in the main panel you can have a fraction of the asset events that have been generated so far directly on your homepage.
![[Pasted image 20251004145657.png]]
Airflow **Assets** (also known as **Data-Aware Scheduling**) is a feature that allows your Directed Acyclic Graphs (DAGs) to be scheduled and triggered based on the **creation or update of data** rather than just time. It helps manage data dependencies across your workflow ecosystem.

In the DAGs view you can have the list of all DAGs in your airflow instances.  In the Search shit space that a forgot the name, you can type part of the DAG that you looking for and find it more easily, under the bar you have different states of the DAGs:
![[Pasted image 20251004150223.png]]