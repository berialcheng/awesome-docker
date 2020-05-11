

# Get started
0. `docker-compose up -d`
1. 
    ```
    docker run -it --rm --network kafka_default \
    -e KAFKA_CFG_ZOOKEEPER_CONNECT=zookeeper:2181 \
    bitnami/kafka:latest kafka-topics.sh --list --zookeeper zookeeper:2181
    ```
    * docker-compose exec zookeeper zkCli.sh
2. 
    ```
    docker run -it --rm \
        --network kafka_default \
        -e KAFKA_CFG_ZOOKEEPER_CONNECT=zookeeper:2181 \
        bitnami/kafka:latest bash
    ```
    * kafka-topics.sh --create --zookeeper zookeeper:2181 --topic mytopic --partitions 3 --replication-factor 1
    * kafka-topics.sh --list  --zookeeper zookeeper:2181
    * kafka-topics.sh --describe --zookeeper zookeeper:2181 --topic mytopic
    * kafka-console-producer.sh --broker-list kafka:9092 --topic mytopic
    * kafka-console-consumer.sh --bootstrap-server kafka:9092 --topic mytopic --from-beginning
3. 
    * docker-compose exec kafkacat kafkacat -b kafka:9092 -L
    * docker-compose exec kafkacat kafkacat -b kafka:29092 -L

# References
* [bitnami kafka image](https://hub.docker.com/r/bitnami/kafka)
* [bitnami zookeeper image](https://hub.docker.com/r/bitnami/zookeeper)
* [Kafka Listeners - Explained](https://rmoff.net/2018/08/02/kafka-listeners-explained/)
* [Kafka listener vs advertised.listeners](https://stackoverflow.com/questions/42998859/kafka-server-configuration-listeners-vs-advertised-listeners#answer-43000344)
* [Kafkacat ](https://hub.docker.com/r/solsson/kafkacat)
