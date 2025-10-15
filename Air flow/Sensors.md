The purpose of a Sensor is to wait for an event.

That can be useful for many different use cases, such as:

- Processing files from an S3 bucket as they arrive while waiting for them.
- Running different tasks at different times but within the same DAG.
- Triggering a data pipeline when another one completes.
- Ensuring an API is available to make requests.
- Transforming data as soon as data are present in a SQL table.

Airflow provides numerous Sensors that cover a wide variety of use cases.  
If you want to wait for an event before doing something, go to the [Astronomer Registry](https://registry.astronomer.io/), search for the service you interact with, and look for the sensors.

A Sensor is a particular operator that waits for a condition to be true. If the condition is true, the task is marked `successful` , and the next task runs. If the condition is false, the sensor waits for another interval until it times out and `fails`.

Implementing a Sensor is as simple as shown below:

```python
from airflow import DAG
from airflow.sensors.python import PythonSensor

def _condition():
    return False

with DAG(
    dag_id="sensor",
    start_date=datetime(2021, 1, 1),
    schedule="@daily",
    catchup=False,
):
    waiting_for_condition = PythonSensor(
        task_id="waiting_for_condition",
        python_callable=_condition,
        poke_interval=60,
        timeout=7 * 24 * 60 * 60
    )
```

AWS exemple:
```python
from airflow.providers.amazon.aws.sensors.s3 import S3KeySensor

@dag(
	scheduler = None,
	start_date=datetime(2023, 1, 1),
	tags=['aws'],
)

	def my_dag():
		wait_for_file = S3KeySensor(
		task_id="wait_for_file",
		aws_conn_id="aws_s3",)
		bucket_key="s3://marc-airflow/data_*",)
		wildcard_match=True,
	
	@task
	def process_file():
		print("I processed the file!")
		
	wait_for_file >> process_file()
	
my_dag()
```

**S3KeySensor** allows you  to wait for a file, in this case, a file starting with `data_*` in the bucket `marc-airflow`. As soon the file is found, the next task process file will be executed.

Keep in mind that while the sensor is waiting, it is taking a worker slot. That can become an issue if you have a limited number of slots and many sensors.


## Practice: Better utilize Sensors
Sensors are designed to wait for something to happen.

By default, a sensor waits for 7 days before timing out, which can lead to an issue... Not being able to run any more tasks!

In this activity, you will learn:

- Best practices around Sensors
- How to avoid freezing your entire Airflow instance
- Better optimize resources to execute more tasks and lower your infra costs

### Prerequisites

To follow the activity, you have two options:

- Running a Sandbox environment in the Cloud with Github Codespaces (Github account required)
- Running a local development environment with the Astro CLI

To set up your environment, go to the following [repo](https://github.com/astronomer/education-sandbox) and look at the Readme

Ready? let's go!

### Practice

To show you what happens if you run too many Sensors without being careful with your resources, open `.env` and add the following value:

`AIRFLOW__CORE__PARALLELISM=3`

This environment variable overwrites the parallelism to limit the maximum number of concurrent tasks to 3. That means you can't have more than 3 tasks running in parallel.

In the folder dags, create a new file fist_dag.py

```python
from airflow.decorators import dag, task
from airflow.sensors.filesystem import FileSensor
from datetime import datetime

@dag(
    schedule=None,
    start_date=datetime(2023, 1, 1),
    tags=['sensor'],
    catchup=False
)
def first_dag():

    wait_for_files = FileSensor.partial(
        task_id='wait_for_files',
        fs_conn_id='fs_default',
    ).expand(
        filepath=['data_1.csv', 'data_2.csv', 'data_3.csv']
    )

    @task
    def process_file():
        print("I processed the file!")

    wait_for_files >> process_file()

first_dag()
```

This DAG runs three FileSensor, each waiting for data_1.csv, data_2.csv, and data_3.csv, respectively.

Since the FileSensor needs a connection that contains the path where the files we're waiting for will be, we must create this connection `fs_default`

Open `airflow_settings.yaml` and create the following connection

```markup
airflow:
  connections:
    - conn_id: fs_default
      conn_type: File (path) 
      conn_host:
      conn_schema:
      conn_login:
      conn_password:
      conn_port:
      conn_extra:
        path: /usr/local/airflow/include/
```

Finally, create new file `second_dag.py` in the folder dags

```python
from airflow.decorators import dag, task
from airflow.sensors.filesystem import FileSensor
from datetime import datetime

@dag(
    schedule=None,
    start_date=datetime(2023, 1, 1),
    tags=['sensor'],
    catchup=False
)
def second_dag():

    @task
    def runme():
        print("Hi")

    runme()

second_dag()
```

Once you have everything set up, restart the Airflow instance with `astro dev restart` in the terminal.


## Questions

Question 1:  
Manually trigger the DAG `first_dag`, wait for having 3 tasks running then trigger the DAG `second_dag`.

![](https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2F7h36gmbsngcalrhewydd1m489%2Fpublic%2F1684848115%2FScreenshot+2023-05-23+at+17.20.32.1684848114670.png)

What's the task's state of `runme` in `second_dag`?

 running

 queued

 ==scheduled==
____
Question 2:
How many worker slots are used?

 ==3==

 2

 1
___

Question 3:
Turn off the schedule of both DAGs and delete the two DAG runs by going to Browse and DAG Runs.

The DAG view should look like that:

![](https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2F7h36gmbsngcalrhewydd1m489%2Fpublic%2F1684848495%2FScreenshot+2023-05-23+at+17.28.03.1684848494715.png) Now,

1. Open the file `first_dag.py`
2. Add a new parameter `mode='reschedule'` in `partial()`
3. Save the file
4. Manually trigger `first_dag`

What is the status of the three tasks waiting_for_files?

 scheduled

 queued

 running

 ==up_for_reschedule==
____

Question 4:  
How many worker slots are running?

 1

 ==0==

 3
____

Question 5:  
Manually trigger the DAG `second_dag`.

Does the task `runme` run?

 ==Yes==

 No
____

Question 6:  
Create a new empty file `data_1.csv` in the folder `include`

![](https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2F7h36gmbsngcalrhewydd1m489%2Fpublic%2F1684849071%2FScreenshot+2023-05-23+at+17.37.43.1684849071602.png)

Go back to the Airflow UI and wait a minute.

What do you see?

 Nothing

 3 tasks are still up_for_reschedule

 ==1 sensor has been successfully executed==
 
 ![[sensor_activity.zip]]

```python
from airflow.decorators import dag, task
from datetime import datetime
import requests

from airflow.sensors.base import PokeReturnValue


@dag(start_date=datetime(2022, 12, 1), schedule="@daily", catchup=False)
def sensor_decorator():

    @task.sensor(poke_interval=30, timeout=3600, mode="poke")
    def check_shibe_availability() -> PokeReturnValue:
        r = requests.get("http://shibe.online/api/shibes?count=1&urls=true")
        print(r.status_code)

        if r.status_code == 200:
            condition_met = True
            operator_return_value = r.json()
        else:
            condition_met = False
            operator_return_value = None
            print(f"Shibe URL returned the status code {r.status_code}")

        return PokeReturnValue(is_done=condition_met, xcom_value=operator_return_value)

    # print the URL to the picture
    @task
    def print_shibe_picture_url(url):
        print(url)

    print_shibe_picture_url(check_shibe_availability())


sensor_decorator()
```


## Best practices with Sensors

When using sensors, keep the following in mind to avoid potential performance issues:

- Always define a meaningful `timeout` parameter for your sensor. The default for this parameter is seven days, which is a long time for your sensor to be running. When you implement a sensor, consider your use case and how long you expect the sensor to wait and then define the sensor's timeout accurately.
- Whenever possible and especially for long-running sensors, use the `reschedule` mode so your sensor is not constantly occupying a worker slot. This helps avoid deadlocks in Airflow where sensors take all of the available worker slots.
- If your `poke_interval` is very short (less than about 5 minutes), use the `poke` mode. Using `reschedule` mode in this case can overload your scheduler.
- Define a meaningful `poke_interval` based on your use case. There is no need for a task to check a condition every 60 seconds (the default) if you know the total amount of wait time will be 30 minutes.

## Questions


Question 1: 
A Sensor can be used for (**Choose all that apply**):

 ==waiting for files to appear in an S3 bucket==

 ==waiting for a task in another DAG to complete==

 ==waiting for data be present in a SQL table==

 ==waiting for a specified data and time==
____

Question 2:  
You have a sensor that waits for a file to arrive in an S3 bucket. Your DAG runs every 10 mins, and it takes 8 mins to complete.

What is the **most** appropriate timeout duration for the sensor? (in seconds)

 60 * 60 * 24 * 7

 60 * 60

 ==60 * 5==

Question 3:  
What mode doesn't take a worker slot while a Sensor waits?

 poke

 ==reschedule==

 none
____

Question 4:  What Sensor(s) can be used to apply logic conditions? (**Choose all that apply**)

 ==PythonSensor==

 == @task.sensor==

 S3KeySensor
___

Question 5: 
Go on the Airflow doc [here](https://airflow.apache.org/docs/apache-airflow/stable/_modules/airflow/sensors/base.html#BaseSensorOperator) and tell me:
![[Pasted image 20251014152924.png]]

What parameter can be useful to check for data to be present in a database without putting too much workload on each poke?

 timeout

 ==exponential_backoff==

 mode