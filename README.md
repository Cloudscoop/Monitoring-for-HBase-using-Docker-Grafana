# Monitoring-for-HBase-using-Docker-Grafana

**Environment:**
JDK 1.8.0_162
CentOS 6.6
Hadoop 2.7.3
HBase 2.0-alpha4


**How To Build Docker Images**

docker-compose -f build-images.yml build

**How To Start Container**
docker-compose up -d

And you would get the list of containers:

Check using docker ps comamnd

master
slave1
slave2



Environment:
JDK 1.8.0_162
CentOS 6.6
Hadoop 2.7.3
HBase 2.0-alpha4


How To Build Docker Images

docker-compose -f build-images.yml build

How To Start Container
docker-compose up -d

And you would get the list of containers:

master
slave1
slave2



**How To Operating HBase In Container After All Containers**


Log into container of hbase master via below command:

docker exec -it master bash


**Using HBase shell:**

hbase shell


**How To Starting All Containers After Stop**
docker-compose start



Check Service Web UI

HBase:http://{hostip}:16010
Hadoop:http://{hostip}:50070
Yarn Application:http://{hostip}:8088

Note: {hostip} is the ip of your host node. If your host ip is 192.168.1.78, you could access the HBase web ui via http://192.168.1.78:16010


**Get Data into HBase for testing:
**

