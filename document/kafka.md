Kafka
==================

- Topic 생성
> /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --topic bigdata --zookeeper localhost:2181 --partitions 3 --replication-factor 1

<br>

- Topic 확인
> /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --describe --topic bigdata --zookeeper localhost:2181

<br>

- Produce Data
> /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --topic bigdata --broker-list sandbox.hortonworks.com:6667

<br>

- Consume Data
> /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --topic bigdata --zookeeper localhost:2181

<br>

- Offset Checker
> /usr/hdp/current/kafka-broker/bin/kafka-consumer-offset-checker.sh --topic bigdata --group console-consumer-* --zookeeper localhost:2181
