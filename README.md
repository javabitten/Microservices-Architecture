# Microservices-Architecture

![architecture](https://user-images.githubusercontent.com/52471507/128783666-bcd7ffa5-a6aa-406e-8752-c4141bf6cf3f.PNG)

**Step 1:
Create User Rest API:**


![image](https://user-images.githubusercontent.com/52471507/128786519-064732c5-858b-42cf-b7fc-1735b888d420.png)
![image](https://user-images.githubusercontent.com/52471507/128786946-b061b268-f761-454d-9887-bb8a84bfdf1a.png)

**Rest Template** is used to create applications that consume RESTful Web Services. 
You can use the exchange() method to consume the web services for all HTTP methods.
Spring Boot REST template was created to simplify REST services consumption in a Spring Boot application.

![image](https://user-images.githubusercontent.com/52471507/128787363-f4e70e72-2df2-4652-987d-f104cc901656.png)

![image](https://user-images.githubusercontent.com/52471507/128787471-e02a946d-82b8-46aa-bca8-e849dc8c0072.png)

**create the Department API similarly**


We have two applications/REST APIs working now.


**APP 3: Service Registry**

How do clients of a service (in the case of Client-side discovery) and/or routers 
(in the case of Server-side discovery) know about the available instances of a service? 

Implement a service registry, which is a database of services, their instances and their locations. 
Service instances are registered with the service registry on startup and deregistered on shutdown. 

Create a new App and named it as: service-registry
add the following dependency: **EUREKA SERVER**

![Eureka Server](https://user-images.githubusercontent.com/52471507/128788132-cfecb342-fb56-407b-a0d0-9fe85083c0c5.PNG)

**Eureka Server (service-registry-config)**

![Eureka Server (service-registry-config)](https://user-images.githubusercontent.com/52471507/128788193-771bd713-8525-4455-9e59-d0e2540b8e3e.PNG)

**Eureka Server** is an application that holds the information about all client-service applications. 
Every Micro service will register into the Eureka server and Eureka server knows all the client applications running on each port and IP address. 
Eureka Server is also known as **Discovery Server**.


Now we have Eureka Server up and running we need to have the Eureka client on the APP1 & APP2:

Eureka Discovery Account(add in the POM of the user and department)

![Eureka Discovery Account(add in the POM of the user and department)](https://user-images.githubusercontent.com/52471507/128788423-789fce01-e7a2-4c7b-8f9a-d0fd58d03b34.PNG)

the port # 8761 is the port number of the eureka server of the **APP 3 --> **service-registry****

![Eureka Discovery Account Config](https://user-images.githubusercontent.com/52471507/128788438-ae784679-f545-4625-af58-e85ac7a80b7c.PNG)

APP 4: **API Gateway**

new application first we need this app to connect to service registry 
therefore we will add dependency Eureka discovery client
getway dependency
actuator dependencies
	
Now we have to do the routing configuaration i.e. all the urls(predicates) with department in it should be routed to DEPARTMENT api

![image](https://user-images.githubusercontent.com/52471507/128789082-221ad4dd-4234-41f7-be84-6a31cdd68261.png)


Circut breaker:
which of the srevices are not working and will run the fall back methods and notify the users that this service is not sorking.

we will implement the Hystrix libraries and dashboard so that we could identify which service is down.


**APP 5: GIT HUB Repo for Common Configs**

Eureka client config are common for all the applications arround our application context, we will create a new app named CloudConfigServer

we have created the .yml file and put repo github link into it.
![image](https://user-images.githubusercontent.com/52471507/128887237-7dceac0e-b056-4b97-a5e0-d313e68d651b.png)

![image](https://user-images.githubusercontent.com/52471507/128887159-4f2bbc2a-4b77-4371-b40d-a754730190bf.png)


Now add the following dependency in the user app, department app, service registry, api gateway and hystrix dashboard api


![image](https://user-images.githubusercontent.com/52471507/128891125-cfa8de30-1c94-425c-b982-fb9a623bb9fe.png)

Now create bootsrap.yml file in all the api's and paste the following there.
p.s 9296 is the port number of the **APP 6: GIT HUB Repo for Common Configs**

![image](https://user-images.githubusercontent.com/52471507/128891478-082a9ee6-1359-46c9-8440-ddc0a64200a8.png)




Distributed Log Tracing:

 you are sending one request and that one particular request is traverse to many APIs.
to trace if there is any or many error is very difficult:

