## KAFKA

1. 2.0
2. Created by Linkedln
3. Horizontal scalability
4. Use Case
    - Messaging system
    - Activity Tracking
    - Gather metrics from many different locations
    - Application logs gathering
    - Stream processing ( with kafka streams api or spark)
    - de coupling of system dependencies
    - Integration with another big data thechnologies
5. Real time insights


**Topics, partitions and offsets**

1. Topics: a particular stream of data
2. Similar a table
3. Topics are split in partitions
4. Each message within partition gets an incremental id, called offset
5. Data is kept only for a limited time, default is one week
6. Data is immutable if written to a partition


**Brokers**

1. Same as servers
2. Kafka cluster is composed of multiple brokers
3. Each broker is idenfitied with its id, and containe certain topic partitions

**Topic replication factor**

1. Topics shold have a replication factor > 1 (usually between 2 and 3)
2. This way if a broker is down, another broker can serve the data
3. Can be a leader on partition
4. Zookeeper define the  leader partition

**Producers**

1. producers write data to topics
2. producers automatically know to wich broker and paritition to write to
3. in case of broker failures producer will automatically recover
4. producers can shoose to receive acknowledgment of data writes, that means response from brokers
5. Message keys, producer can shoose to send a key with the message
5. Message keys is sent if you  need message ordering, for specific field

**Cosumers**

1. Read data from topic
2. Cosumers know withc broker to read from
3. Data is read in order withn each partitions
4. Consumer groups, read data in consumer groups
5. if you have more consumers than partitions, some consumers will be inactive


**Consumer offsets**

1. Kafka store the offset at wich a consumer gorup has benn reading
2. __consumer_offsets
3. If consumer dies, it will be able to read back from where it left off
4. commit at most once
5. commit at least once
6. commit exactly once


**Kafka broker discovery**

1. Every kafka broker is also called a bootstrap server
2. That means that you only need to conect to one broker, and you will be connected to entire cluster

**Zookeeper**

1. Zookeeper manages brokers
2. Zookeeper helps in performing leader electiono of partitions
3. Zookeeper send notifications to kafka in case of changes
4. Kafka cant work without zookeeper
5. Zookeeper by desing operates with an odd number, e.g 3,5,7


## Install

1. Java 8
2. Kafka 2.0
3. Add bin folder to environment
4. Create data folder on root kafka
    - Create kafka, zookeeper folders
5. Copy location of zookeeper
6. Go to config folder, open zookeeper.properties
7. Change data folder
8. Go to config folder, opzen server.properties
9. Change log.dirs to kafka data folder, already created

**Start**

1. `zookeeper-server-start kafka_2.12-2.0.0\config\zookeeper.properties`
2. ``


**CLI**

1. `kafka-topics --zookeeper 127.0.0.1:2181 --topic first_topic --create --partitions 3 --replication-factor 1`
2. `kafka-topics --zookeeper 127.0.0.1:2181 --list`
3. `kafka-topics --zookeeper 127.0.0.1:2181 --topic first_topic --describe`
4. `kafka-topics --zookeeper 127.0.0.1:2181 --topic descond_topic --delete`
5. `kafka-console-producer --broker-list 127.0.0.1:9092 --topic first_topic`
6. `kafka-console-producer --broker-list 127.0.0.1:9092 --topic first_topic --producer-property acks=all`
7. If send message to topic not existed, this topic will be created
8. `kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic`
9. `kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --from-beginning` show all messages already sended
10. Consumers in group `kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --group my-first-app`, can be multiples consumers
11. `kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --group my-first-app --from-beginning`
12. If consumer is not running, messages send on this time, will be show on next consumer execution
13. `kafka-consumer-groups --bootstrap-server localhost:9092 --list`
14. Reset offsets `kafka-consumer-groups --bootstrap-server localhost:9092 --group my-frist-application --reset-offsets --to-earliest --execute --topic first_topic`
15. `kafka-consumer-groups --bootstrap-server localhost:9092 --group my-frist-application --reset-offsets --shift-by 2 --execute --topic first_topic`


**Kafka GUI**

1. https://www.conduktor.io/


**In Java**



**Twitter example**

1. Developer account
2. Java Code to retrieve from webhook twitter, all messages pass on listener will be send to a producer
3. The code send by producer will be listened by consumer
4. Consumer can be save on disk, save on database, process in real time, etc


**ELK**

1. Use at least once, if goes wrong try send again.


**Extends APIs**

1. Usgin connector for kafka
2. Twitter connector is an example

**Kafka Streams**

1. Data processing and transformation library within kafka
2. Fraud Detection
3. Monitoring and alerting
4. https://medium.com/@stephane.maarek/the-kafka-api-battle-producer-vs-consumer-vs-kafka-connect-vs-kafka-streams-vs-ksql-ef584274c1e



**Others**

1. Message Compression
2. Replication factor should be at least 2, usually 3, maximum 4
3. Never set to 1 in production
4. https://medium.com/@criccomini/how-to-paint-a-bike-shed-kafka-topic-naming-conventions-1b7259790073
5. Connector to read direct from database
6. https://kafka.apache.org/documentation/#monitoring
7. https://docs.confluent.io/platform/current/kafka/monitoring.html
8. https://www.datadoghq.com/blog/monitoring-kafka-performance-metrics/
