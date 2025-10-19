 **For Docker**
 ```bash
 docker ps
 ```
 
 To find the scheduler ID
```bash
docker exec -it <the container id> sh
```
Now your are logged in the scheduler and can run de commands.


**For Kubernetes**
you will also logged in the scheduler
```bash
kubectl exec -it scheduler pod name -- sh
```

**For Astro CLI**
```bash
astro dev run
```

```bash
astro dev bash
```
you already in the scheduler 


## Basic Commands 

To start the metadata database, usually used once
```bash
airflow db init
```

Create Users whit specific access: 
let's say a user that is able to see the environment but not to trigger any workflows
```bash
airflow users create -e <e-mail> -f <name> -l <last name> -u <user name> - <password> -r <the roll, in this case will be..> Viewer
```
the roll can be a: administrator, public, viewer, editor or even a custom role.

in the localhost 8080 you can logger with the new user. And inthe visual tool whit a administrator  user you can set the **custom role**, by clicking in **List Roles** and edit 

**For add role** a already created   user you can use:
```bash
airflow user add-role -e <e-mail> -r <the intended role> Custom
```

To **initialize you bd**, **start your web server** and also your **scheduler** in one go, you can use:
```bash
airflow standalone
```

It's not good use  standalone commend on production, is good practice use only in development purposes.

----
## Airflow Environment 

To **know the version**:
```bash
airflow version
```

To **know all the providers** that has been installed
```bash
airflow info
```

==a celery executor may can not be able to scale the workers==

If  you wanna **get the value of a specific configuration element**:
```bash
airflow config get-value <especify, in this case> core max_active_run_per_dag
```

## Common Commands

to get a **list of most common commands for instance**:
```bash
airflows cheat-sheet
```

To **export and import configurations** -- connections, variables, users and pools to another Airflow environment:
```bash
airflow pools export

airflow roles export

airflow variables export

#and so on 
```
 you on would see variables that is in the .env file.

## Test your tasks

Ensuring the reliability and accuracy of tasks within your DAG is crucial. Testing is vital in achieving this, allowing you to validate task functionality, identify potential issues, and maintain data integrity before running the DAG or pushing it into production.

One command that you must always use is: `airflow tasks test <dag_id> <task_id> <logical_date>`

This command runs a task without checking for dependencies or recording its state in the database. For example, if the task pushes an XCOM, the XCOM won't be created with that command.

Let's imagine you have the DAG below:

```python
from airflow.decorators import task, dag
from airflow.exceptions import AirflowException
from datetime import datetime

@dag(start_date=datetime(2023, 1, 1), schedule=None, catchup=False)
def cli():

    @task
    def my_task(val):
        print(val)
        return 42

    my_task(80)
cli()
```

To test the task `my_task` , execute the command: `airflow tasks test cli my_task 2023-01-01`. You should see:

```markup
[2023-06-14T12:38:50.188+0000] {taskinstance.py:1545} INFO - Exporting env vars: AIRFLOW_CTX_DAG_OWNER='airflow' AIRFLOW_CTX_DAG_ID='cli' AIRFLOW_CTX_TASK_ID='my_task' AIRFLOW_CTX_EXECUTION_DATE='2023-01-01T00:00:00+00:00' AIRFLOW_CTX_TRY_NUMBER='1' AIRFLOW_CTX_DAG_RUN_ID='__airflow_temporary_run_2023-06-14T12:38:50.069609+00:00__'
80
[2023-06-14T12:38:50.189+0000] {python.py:183} INFO - Done. Returned value was: 42
[2023-06-14T12:38:50.196+0000] {taskinstance.py:1345} INFO - Marking task as SUCCESS. dag_id=cli, task_id=my_task, execution_date=20230101T000000, start_date=, end_date=20230614T123850
```

Two important notes:

1. `Marking task as SUCCESS` shows that the task works and has been successfully executed
2. `Returned value was: 42` indicates that the tasks created a XCOM with the value 42. However, if you look into admin and XCOMs, you will see that nothing has been created. That's because airflow tasks test do not store any task related metadata.

Try to execute the following code and see what you get:

```python
from airflow.decorators import task, dag
from airflow.exceptions import AirflowException
from datetime import datetime

@dag(start_date=datetime(2023, 1, 1), schedule=None, catchup=False)
def cli():

    @task
    def my_task(val):
        raise AirflowException()
        print(val)
        return 42

    my_task(80)
cli()
```

As a best practice, each time you add a task in a DAG, test it with `airflow tasks test`.

## Practice: Backfill your DAG without the CLI

# Introduction

---

- If you don’t have access to the CLI, there is no direct backfill method.
- However it is possible by triggering a `backfill_trigger_dag` via the API and using `dag_run.conf` to pass in parameters such as `start_date`, `end_date`, and `dag_id` for the required backfill.
- the `backfill_trigger_dag` will then trigger the backfill for the desired _target_ DAG
- ensure the `backfill_trigger_dag` is unpaused, with a schedule of `None` so that it can be triggered as needed but does not run on an interval

# Prerequisites

---

- Airflow CLI installed

# Instructions

---

**→ In the below example, we will use two DAGs:**

1. The `backfill_trigger_dag` - this DAG uses a `BashOperator` to run the Airflow CLI command `airflow dags backfill` and pulls in the `dag_run.conf` values that we pass while manually triggering on the UI i.e `start_date`, `end_date`, `dag_id`, etc.
2. The `example_dag_basic` - this is the DAG the backfill is being performed on (i.e. the _target_ DAG). You can backfill any DAG of your choice.

**→ The DAG responsible for triggering the backfill:**

**`backfill_trigger_dag`:**

> 💡 **Note:** We will use Jinja templates to pull in the `dag_run.conf` values from the API call:

```python
from airflow import DAG
from airflow.operators.bash import BashOperator
from datetime import datetime

with DAG(dag_id='backfill_trigger_dag',
         schedule_interval=None,
         start_date=datetime(2022, 1, 1),
         tags=['backfill-trigger-cli'],
         catchup=False) as dag:

    # Use the UI to trigger a DAG run with conf to trigger a backfill, passing in start/end dates and dag_id etc:
    trigger_backfill = BashOperator(
        task_id='trigger_backfill',
        bash_command="airflow dags backfill --reset-dagruns -y -s {{ dag_run.conf['date_start'] }} -e {{ dag_run.conf['date_end'] }} {{ dag_run.conf['dag_id'] }}"
    )

    trigger_backfill
```

**→ The execution will be as follows**

1. First we shall manually trigger the **`backfill_trigger_dag`** with a configuration json.

![](https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2F2xu4phg6iib0aa8xnxkbau3kg%2Fpublic%2F1681150028%2FUntitled.1681150027767.png)

2. Now we shall pass the necessary parameters for performing the backfill including

    →`dag_id`

    →`date_start`

    →`date_end`

    i.e `{"dag_id": "example_dag_basic", "date_start": 20230401, "date_end": 20230405}`

![](https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2F2xu4phg6iib0aa8xnxkbau3kg%2Fpublic%2F1681150080%2FUntitled.1681150079720.png)

3. And we get the 5 backfills successfully

![](https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2F2xu4phg6iib0aa8xnxkbau3kg%2Fpublic%2F1681150108%2FUntitled.1681150108416.png)

4. We can verify the same from the Browse → DAG Runs tab as well

![](https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2F2xu4phg6iib0aa8xnxkbau3kg%2Fpublic%2F1681150134%2FUntitled.1681150134427.png)

**Great! Now we can backfill a DAG even if we don’t have access to the Airflow CLI.**

## Questions
Question 1: 
What is the purpose of airflow db init and when might you use it?

 Creates a new user in Airflow

 Generates a report of all DAGs currently in your Airflow environment

 Starts the Airflow web server

 ==Initializes the Airflow metadata database, typically used when setting up Airflow for the first time==
____

Question 2:  
What is the use case for airflow config get-value and how might you use it to troubleshoot issues?

 Lists all of the DAG files that have failed to import

 ==Retrieves the value of a specific configuration option, useful for verifying that configuration settings are correctly set==

 Verifies the validity of the Airflow metadata database schema

 Reserializes a DAG file to ensure that it can be properly loaded by Airflow
____

Question 3: 
You've recently upgraded your Airflow installation, but now your DAGs is not showing up in the UI. Which commands could you use to identify any import/parsing errors that might be preventing the DAG from being loaded?

 ==airflow dags list-import-errors==

 airflow dags show

 ==airflow dags report==

 airflow dags backfill
____

Question 4:
Why would you use Airflow's backfill functionality?

 To test DAGs before deploying them to a production environment

 To reschedule a DAG to run at a different frequency

 ==To fill in missing historical data that was not previously captured==

 To remove all past DAG runs and start fresh with a new schedule
___

Question 5: 
What does the `airflow db check` command do?

 Upgrades the Airflow database schema to the latest version

 ==Checks the connection to the Airflow database==

 Removes all data from the Airflow database

 Initializes the Airflow database
 ____

## References

**References**

1. [Local Development Environment](https://academy.astronomer.io/local-development-environment)
2. [Environment Variables](https://academy.astronomer.io/astro-module-environment-variables) 
3. [Airflow Configuration](https://airflow.apache.org/docs/apache-airflow/stable/configurations-ref.html)
4. [CLI Commands](https://airflow.apache.org/docs/apache-airflow/stable/cli-and-env-variables-ref.html)
5. [Astro CLI](https://docs.astronomer.io/astro/cli/reference)
6. [Airflow Variables](https://academy.astronomer.io/astro-runtime-variables-101)
7. [Airflow Connections](https://academy.astronomer.io/connections-101)
8. [Debugging DAGs](https://academy.astronomer.io/debug-dags)