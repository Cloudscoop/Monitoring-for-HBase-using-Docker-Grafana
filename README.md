# Monitoring-for-HBase-using-Docker-Grafana

**Environment:**
JDK 1.8.0_162
CentOS 6.6
Hadoop 2.7.3
HBase 2.0-alpha4



##**How To Build Docker Images** (Optional)

`docker-compose -f build-images.yml build`



##**How To Start Container**

`docker-compose up -d`

And you would get the list of containers:

Check using `docker ps` comamnd

master

slave1

slave2



##**How to check HBase**


Log into container of hbase master via below command:

`docker exec -it master bash`


**Using HBase shell:**

`hbase shell`


##Check Service Web UI

HBase:http://{Public IP}:16010
Hadoop:http://{Public IP}:50070
Yarn Application:http://{Public IP}:8088

Note: {Public IP} is the ip of your host node. If your host ip is 192.168.1.78, you could access the HBase web ui via http://192.168.1.78:16010


##******Troubleshooting:******


**How To Starting All Containers After Stop**

`docker-compose start`




#**Get Data into HBase for testing:
Log into Master using ,`docker exec -it master bash`

hdfs dfs -ls /
vi importsv
rowkey000000000,Test1,Test2,Test3,Test4,Test5,Test6,Test7,Test8,Test9,Test10
hdfs dfs -copyFromLocal importsv /tmp/
hdfs dfs -ls /tmp/
    
hbase shell
    
create 'bktable', {NAME => 'cf'},   {SPLITS => ['rowkey033333333', 'rowkey066666666']}
    
list
exit
     
hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns=HBASE_ROW_KEY,cf:c1,cf:c2,cf:c3,cf:c4,cf:c5,cf:c6,cf:c7,cf:c8,cf:c9,cf:c10 -Dimporttsv.skip.bad.lines=false '-Dimporttsv.separator=,' -Dimporttsv.bulk.output=hdfs://master:9000/tmp/bktableoutput bktable hdfs://master:9000/tmp/importsv


hbase org.apache.hadoop.hbase.tool.LoadIncrementalHFiles hdfs://master:9000/tmp/bktableoutput bktable

hbase shell
list
