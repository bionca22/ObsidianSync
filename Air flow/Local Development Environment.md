 ```bash
 astro dev logs --webserver
 
 astro dev logs --scheduler 
 ```
Access the logs of different Airflow components.

```bash
astro dev pytest
```
 Executa os testes.

```bash
astro dev restart 
```
Restart your environment.

## Alternatives 

python package index (pip)
Docker/ Doker Compose
Released Sources
Helm Chart
 
astro version 


### Local Airflow directories

![[Pasted image 20251001173143.png]]

**dags directory:** where you can put your python files corresponding to your data pipelines. Inside him you have two exemples of DAGs that can try and run.

**include:** Here you can put your hard code to SQL query, bash script or python function and than call the SQL request from your data pipeline, so your code remain clear as possible.

**plugins:** to customize the Airflow user interface you will need to create a file and then add a new operator or change the UI, and it goes on plugins directory.

**tests:** with you are familiar with the pytest, this is something you can do with Astro CLI.

**.dockerignore:** that describes the files and folders that you want exclude from the Docker image when you build it. 

**.env:** let's say you want to configure your Airflow instances, then you can use environment variables for that using this file.

**.gitignore:** to ignore some files that you don't want to go on your git repository 

**airflow_settings:** As you know, as you are using a local development environment, you may need to destroy it and recreate it, but you don't want to lose the data or the configuration settings that you've defined. you can use that file for that by hard coding your settings like connections, variables, and so on in that file, you not gona lose them each time you create your environment.

**Dockerfile:** Used to build your Docker image, and so running airflow.
![[Pasted image 20251001175646.png]]
as you can see in this image  the Astro runtime Docker image, it's good keep the version updated to the latest version of airflow.

**packages.txt:** let's say you want to install a operating system package, wget or something else than you can do that just by typing the package you want to install in your Airflow environment, and then it will be available to your data pipeline. Like that: 
![[Pasted image 20251001180259.png]]
