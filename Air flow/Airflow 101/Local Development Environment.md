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

📁**dags directory:** where you can put your python files corresponding to your data pipelines. Inside him you have two exemples of DAGs that can try and run.

📁**include:** Here you can put your hard code to SQL query, bash script or python function and than call the SQL request from your data pipeline, so your code remain clear as possible.

📁**plugins:** to customize the Airflow user interface you will need to create a file and then add a new operator or change the UI, and it goes on plugins directory.

📁**tests:** with you are familiar with the pytest, this is something you can do with Astro CLI.

📁 **.dockerignore:** that describes the files and folders that you want exclude from the Docker image when you build it. 

📁 **.env:** let's say you want to configure your Airflow instances, then you can use environment variables for that using this file.

📁 **.gitignore:** to ignore some files that you don't want to go on your git repository 

📁**airflow_settings:** As you know, as you are using a local development environment, you may need to destroy it and recreate it, but you don't want to lose the data or the configuration settings that you've defined. you can use that file for that by hard coding your settings like connections, variables, and so on in that file, you not gona lose them each time you create your environment.

📁**Dockerfile:** Used to build your Docker image, and so running airflow.
![[Pasted image 20251001175646.png]]
as you can see in this image  the Astro runtime Docker image, it's good keep the version updated to the latest version of airflow.

📁**packages.txt:** let's say you want to install a operating system package, wget or something else than you can do that just by typing the package you want to install in your Airflow environment, and then it will be available to your data pipeline. 
![[Pasted image 20251001180259.png]]
You can do that by typing the package you want to install, and then it will be available to your data pipelines. 

## Run a Astro Project
para iniciar um novo projeto
```bash
astro dev init
```
Para inicializar o astro CLI
```bash
astro dev start
```

 para parar o projeto 
 ```bash
 astro dev stop
 ```

para reiniciar do projeto 
```bash
astro dev restart 
```

para encerrar o projeto e iniciar do zero, perdendo assim todos os metadados
```bash
astro dev kill
```

opa, foi tudo em português


## Set up VS Code for Airflow

install the extension **Dev Containers**  to open folders and repositories inside a Docker containers taken advantage off the Visual Studio Code feature set , getting IDE features such as good auto-completion, error warning syntax lighting and so on. 

After that you can open the remote window and looking for **Attach to Running Container...** and there you can set the **scheduler**, soon you will see in the inferior corner the starting of the dev container and the connection to your Airflow instances that runs locale. 

The next step is go to **File** up there in VSCode, **open folder** and put the path **/user/local/airflow** and clic in "ok", Now this new tab is running inside the container.

----
Review
**Install Airflow**

- There are two primary ways to install Airflow on a local machine: Python Package Index or Containerization Solutions (e.g., Docker, Podman)

- The Python Package Index

- This method is great for anyone who is comfortable with Python and Python environments or may only have access to it in their local environment 
- This method does require quite a bit of manual setup to get Airflow working on a local machine

- Containerization Solutions

- This method is great for anyone familiar or already using a containerization solution
- This method may still require a bit of customization to the container if the Airflow installation needs to be fine-tuned

- The [Astro CLI](https://github.com/astronomer/astro-cli) is an open-source command line interface (CLI) that makes setting up, running, and managing Airflow a breeze. It comes built-in with a handful of features to make it easier to get started quicker. 
- Alternatives to the Astro CLI include using the Airflow CLI, which is built-in to Airflow, or another open-source project called [AirflowCTL](https://github.com/kaxil/airflowctl)
- Astro CLI can be installed on Mac, Windows, and Linux machines by following the instructions listed in the [documentation](https://docs.astronomer.io/astro/cli/install-cli).

**Set up and Run an Airflow Project**

- To set up a new Airflow project with the Astro CLI, make a new folder, and then use the command **`astro dev init`** to generate a new project.
- The Astro CLI will generate a project with a standard project directory. This includes:

- **The dags directory**: Contains Python files corresponding to data pipelines, including examples such as example_dag_advanced and example_dag_basic.
- **The include directory:** Used for storing files like SQL queries, bash scripts, or Python functions needed in data pipelines to keep them clean and organized.
- **The plugins directory:** Allows for the customization of the Airflow instance by adding new operators or modifying the UI.
- **The tests directory:** Contains files for running tests on data pipelines, utilizing tools like the pytest library.
- **The .dockerignore file:** Describes files and folders to exclude from the Docker image during the build.
- **The .env file:** Used for configuring Airflow instances via environment variables.
- **The .gitignore file:** Specifies files and folders to ignore when pushing the project to a git repository, useful for excluding sensitive information like credentials.
- **The airflow_settings.yaml file:** Stores configurations such as connections and variables to prevent loss when recreating the local development environment.
- **The Dockerfile:** Used for building the Docker image to run Airflow, with specifications for the Astro runtime Docker image and the corresponding Airflow version.
- **The packages.txt file:** Lists additional operating system packages to install in the Airflow environment.
- **The README file:** Provides instructions and information about the project.
- **The requirements.txt file:** Specifies additional Python packages to install, along with their versions, to extend the functionality of the Airflow environment.

- The Astro CLI can be used to run an Airflow project. To start an Airflow project with the Astro CLI, use the command `**astro dev start**`. To restart the project, use **`astro dev restart`**, and to stop the project, use the command **`astro dev stop`**.
- To get Airflow to work with VSCode and provide benefits like correct syntax highlighting and autocompletion, the VSCode instance must be run inside of the docker container using the [Dev Containers](https://code.visualstudio.com/docs/devcontainers/containers) extension.

-----
Question 1:  
What is the purpose of the `airflow_settings.yaml` file in a new Airflow project generated by the Astro CLI?

 For storing Python files corresponding to data pipelines

 ==For storing configurations such as connections and variables to prevent loss when recreating the local development environment==

 For specifying additional Python packages to install, along with their versions, to extend the functionality of the Airflow environment

 For configuring Airflow instances via environment variables

____

Question 2: 
What Astro CLI command will start running a Airflow project?

 ==astro dev start==

----

Question 3: 
What is the purpose of the **include** directory in a new Airflow project generated by the Astro CLI?

 For configuring Airflow instances via environment variables.

 ==For storing files like SQL queries, bash scripts, or Python functions needed in data pipelines to keep them clean and organized==

 For the customization of the Airflow instance by adding new operators or modifying the UI

 For storing configurations such as connections and variables to prevent loss when recreating the local development environment

Question 4:  
Which of the following are benefits of using the Astro CLI for local development? (select all that apply)

 ==To provide a streamlined experience for installing Airflow with limited pre-requisites==

 Its ability to dynamically generate new DAGs using AI

 ==Its ability to generate a standard project directory==

 ==A variety of useful commands for managing an Airflow instance==

Question 5:  Correct answer

What Astro CLI command will generate a new Airflow project? 

 ==astro dev init==