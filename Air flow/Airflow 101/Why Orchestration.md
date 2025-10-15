 **Data orchestration** is the coordination and automation of data floe across various tools and systems to deliver quality data and analytics. 

#### The journey to modern data orchestration

![[Pasted image 20251015105408.png]]

**Pre-unix Era**: 
- Manual batch-processing and scheduling.
- The foundation of the idea and need of data orchestration and workflow management starting to form.
- big lack of standardization of data formats, protocols, and processing techniques.

**Early Computing:**
- Basic time-based scheduling tools.
- A subsequent rise of proprietary scheduling and workload management tools
- Dedicated ETL tooling 

Limitations:
- Proprietary software was expensive, closed-source, and resource intensive.
- Schedulers like Cron and Windows Task Scheduler(WTS) lacked features for more complex workloads and general maintainability.

**Data & Open-Source Renaissance:**
- Increase in data complexity and size.
- Increase in complexity os scheduling and ETL workloads.
- Rise of open-source workflow management projects.

Limitations:
- Some tools were limited to working only within the Hadoop ecosystem.
- Some tools used XML or config files to define workloads.
- Limited dynamism, scalability, and extensibility

**Modern Data Orchestration:**
- Rise of pipelines-as-code in python
- The ability to integrate with hundreds of external systems.
- Time and event-based scheduling
- Feature rich software with built-in observability and a centralized UI.

## Questions
Question 1: 
Which of the following describes the early-computing era of Data Orchestration? (select all that apply)

 Manual processes

 Lack of standards around data formats, processes, and processing techniques

 ==Time-based scheduling tools (e.g., Cron)==

 ==Rise of proprietary scheduling and workload management tools (e.g., AutoSys)==
____

Question 2:  
Which of the following is the definition of modern data orchestration?

 The process of manually handling data flow across different platforms to ensure data security and compliance.

 ==The coordination and automation of data flow across various tools and systems to deliver quality data products and analytics.==

 The exclusive use of a single tool to manage all data-related tasks within an organization.

 The random distribution and storage of data across various databases without any automated processes.
____

Question 3:  
Which of the following describes the pre-unix era of Data Orchestration? (select all that apply)

 Dedicated ETL tooling

 Automated Processes

 ==Lack of standards around data formats, processes, and processing techniques==

 ==Manual and error-prone processes==
___

Question 4:  
Which of the following describes the data and open-source era of Data Orchestration? (select all that apply)

 Adoption of proprietary data formats and protocols to restrict access to data ecosystems

 Manual batch processing

 ==Tools that were designed for specific ecosystems (e.g., Hadoop)==

 ==An increase in data size and complexity of scheduling and workloads==

## Introduction to Airflow

developed by Maxim Beauchemin in 2015

Apache airflow ia an open-source tool for programmatically authoring, scheduling, and monitoring your data pipelines.

The **advantages of Airflow**: 
- Can create pipelines using python.
- Open-source, community driven.
- Observability, count on a monitor manage which provides  managers tasks, DAGs, etc.
- Data awere scheduling, can scheduling your data pipelines based on events.
- Highly extensible, count over a hundred integration packages. It's also possible create your own package.

## Questions 

Question 1:  
Why is Airflow considered the central nervous system of a data stack?

 It functions as a data visualization platform.

 It acts as a standalone tool for data analysis

 ==It connects, coordinates, and manages different tools and systems across a organization's data ecosystem==

 It provides data storage solutions for large datasets.
____

Question 2: 
Which of the following are characteristics of Airflow? (select all that apply)

 Proprietary and closed-source

 ==Extensibility to connect to external systems==

 ==The ability to write pipelines-as-code with Python==

 ==Built-in observability features==


## Who Uses?

**Data Scientist:** Needs to process and analyze new data sets as they arrive, and generate insigths and visualizations automatically.

**Data Engeneer:** Need to resolve the error on yesterday's pipeline run and backfill the data.  

**Machine Learning Engineer:** need my machine learning model to be retrained and validated every time new data is ingested into the system.

**Data Analyst:** Need this report on user growth to be refreshed after every incremental load.

There are four main uses cases where data is bussiness critical.
![[Pasted image 20251015113740.png]]

**Data-Powered Applications:** are programs or systems that rely on data to function and provide value. Like functionalities insights or services to users, And for that exist afitness aplication that provides a user a daily health score and activity goal.

![[Pasted image 20251015114258.png]]
here we got the data sources phone and fitness watch, and then the pipeline in airflow that runs different steps to ingest the data into the data warehouse, to transform the data, run some queries, and export the data  into the production database, so the user can get the health score and the activity goal.


**Critical Operational Processes:** Critical Processes refer to the workflows that are crucial for a business to function. It's all about the essentials workflows that are critical for a business to function.
Like a fraud detection system for transactions made by customers on a e-commerce application.
![[Pasted image 20251015115043.png]]
In that case, you have a pipeline that runs daily in airflow that ingests the transactions from the database, transforms the data, runs machine learning models to detect frauds, and finally generates a report for the compliance team, so they can take actions. 

**Analytics & Reporting:** Analytics and reporting involve the systematic analysis of data to derive insights.So that tams and individuals can make data driven decisions efficiently.
A slackbot that enables staff at Astronomer to check academy data on customer accounts.

![[Pasted image 20251015115814.png]]
So typically we have a customer success manager that sends a message on a specific slack channel with a customer domain and that triggers a pipeline in Airflow that finds the customer, counts the number of students as well as the number of certified students and finally generates reports back to the slack channel. That's how they are able to communicate metrics on customers dor the academy automatically.


**MLOps & AI:** involves the deployment and management of machine learning models within operational workflows.
Ask Astro: A open-source Q&A LLM application used to answer questions about Apache  Airflow & Astronomer.


