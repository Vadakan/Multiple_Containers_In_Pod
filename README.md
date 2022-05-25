# Multiple_Containers_In_Pod

# When we should not go for multiple containers in a pod ? - Specially in microservices architecure we should never use multiple containers in a pod. This affects the basic principle of 'loose-coupling' concept in microservices. Also, if we want to scale one of the microservice, we cannot do that since the containers are inside the pod, if we scale the pod along with our desired microservice, other additional microservice containers inside the pods also will be scaled which is waste and we dont want to do that. so in this scenario multiple containers inside the pod is not a good approach.

# just see the below architecuture where multiple containers inside the pod is not a good approach


![image](https://user-images.githubusercontent.com/80065996/170347049-3399a024-ae54-46f6-a1db-5870c715e308.png)


# Scenario : 1 design pattern for multiple containers in a single pod - "side car" container concept.


![image](https://user-images.githubusercontent.com/80065996/170347369-61ae8233-831e-40c2-ac04-a9b59adac970.png)


 # in above diagram, we could see nginx server which is a web server which will serve the "static data content". also we could see "side car" container which used git to put the static data into the "document root" of "nginx" server so that it serves the static data. 
 # also you could notice, "common volume" us mount for both the containers so that one container writes static data into that ( side car container) and other container will access this data and put it in its "document root" ( niginx container) to server the static data.
 
 # here the main container is "nginx" container. so the side car container is something which just help the main container. only in this type of scenario we have to use multiple containers inside the same pod.
 
 # scenario :2 -- where if application needs "redis-proxy" instead of distributed shards separately.
 
 
 ![image](https://user-images.githubusercontent.com/80065996/170348754-92a3a092-4bbb-4032-be1b-bfb551d604ca.png)


# in above diagram, redis cluster acts as the ambassador for the 'application', it just take the request from 'application' and forwards to necessary shards. That is why it is called 'ambassador' pattern


# Scenario:3 "adapter containers"

![image](https://user-images.githubusercontent.com/80065996/170349373-5527f0d8-476c-440c-bd63-e5ef7586ef15.png)


# in the above diagram, if we need logs from one of the container which is running we can create a shared mount and get the logs into the mount and let other container which is the 'exporter container' which takes these logs and pass it to 'monitoring & alerting' tools like 'prometheus or grafana' or 'splunk' to see what is happening in the apache web server.



# sample application:


![image](https://user-images.githubusercontent.com/80065996/170350170-ce63116d-e832-49e5-9d01-08e058cff6a7.png)




