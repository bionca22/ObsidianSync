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
 you on would see variables that is in the .env file 