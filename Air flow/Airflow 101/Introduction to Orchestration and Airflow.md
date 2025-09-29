
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

