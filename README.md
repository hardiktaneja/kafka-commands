## KAFKA COMMANDS
Kafka Command line is needed to install these commands
Run inside the bin directory of kafka

1. Create a new topic: <br />
```bash ./kafka-topics.sh --create --bootstrap-server kafka-ip:9092 --replication-factor 1 --partitions 500 --topic topicName ```

2. Increase number of partitions <br />
``` bash ./kafka-topics.sh  --bootstrap-server kafka-ip:9092 --alter --topic topicName --partitions  6000 ```

3. Describe Topic - Get info about topic <br />
``` bash ./kafka-topics.sh --describe --zookeeper kafka-ip:2181 --topic topicName ```

4. Delete Topics <br />
``` bash ./kafka-run-class.sh kafka.admin.TopicCommand --delete --topic topicName --bootstrap-server kafka-ip:2181 ```

5. Producer - Enter command wait for '>' to appear, type/paste message to publish and press Enter <br />
``` bash ./kafka-console-producer.sh --broker-list kafka-ip:9092 --topic topicName ```

6. Consumer - Starts from the latest message ie message being published after starting consumer<br />
```bash ./kafka-console-consumer.sh --bootstrap-server kafka-ip:9092 --topic topicName ```<br />

   Consumer - Fetch messages from beginning ie all available messages and keep consuming indefinately<br />
 ```bash ./kafka-console-consumer.sh --bootstrap-server kafka-ip:9092 --topic topicName --from-beginning```<br />
 
   Consumer - Fetch messages from beginning and stop after consuming N messages<br />
  ```bash ./kafka-console-consumer.sh --bootstrap-server kafka-ip:9092 --topic topicName --from-beginning --max-messages=N```<br />
  
 7. Get Lag - Command will generate a big table like structure containing information about cosumers including their IPs and lag on each partition<br />
 ``` bash ./kafka-consumer-groups.sh --bootstrap-server kafka-ip:9092 --describe --group <group-id> ```<br />
 
    Get Lag - Command will generate a single number, containing sum of lag on all partitions<br />
 ``` bash ./kafka-consumer-groups.sh --bootstrap-server kafka-ip:9092 --describe --group <group-name> | grep -E "LAG|*" |  awk '{SUM += $6} END { print SUM}'```<br />
 
 8. Reset offset for a particular consumer group - If you want to go to the start of messages on a topic for a particular consumer group(can replace 0 with any offset number) :<br />
 ```bash ./kafka-consumer-groups.sh --bootstrap-server kafka-ip:9092 --group group-name --reset-offsets --to-offset 0 --topic topic-name --execute ```<br />
 
    Reset offset for a particular consumer group - If you want to go to the end of messages on a topic for a particular consumer group(latest messages) :<br />
  ```bash ./kafka-consumer-groups.sh --bootstrap-server kafka-ip:9092 --group group-name --reset-offsets --to-latest --topic topic-name --execute ```<br />
  
 9. Delete a consumer group<br />
 ```bash ./kafka-consumer-groups.sh --bootstrap-server kafka-ip:9092 --delete --group group-name ```<br />
