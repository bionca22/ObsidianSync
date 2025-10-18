
![[Pasted image 20251015130201.png]]
 A connection in Airflow is composed of some things.

**Unique Connection ID:** a unique identifier or unique connection, you have to specify a unique identifier.

**Set of parameters (login, password, hostname,etc):** that's parameters gona specific the connection type you want to use. For exemple if you use AWS, then you need to specify a secret key and an access key, if you use snowflake you will need to define the computer and so on. It will depend of the connection you wanna use.

**Encrypted:** your connections are encrypted based on the Fernet key, that are specified in your airflow settings

### Create a connection
Through the **Airflow UI**, you go to admin and then, connections. To create a né connection you can clic in the correspond button, an than you have to give a connection ID and pic a connection type. 

If your connection is missing, make sure you have installed the corresponding airflow providers package, so in case the need of install a package, reinitialize the airflow 


### Through line
