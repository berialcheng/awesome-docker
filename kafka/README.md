

# Get started - hellowolrd
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

# Get started - cluster
0. `docker-compose -f docker-compose-cluster.yaml up -d`

# Get started - fullstack
0. `docker-compose -f docker-compose-fullstack.yaml up -d`
1. 
2. `http://localhost:8888/`
```
create schema in;
CREATE TABLE accounts(id SERIAL, name VARCHAR(255));
INSERT INTO accounts(name) VALUES('alice');
INSERT INTO accounts(name) VALUES('bob');
```
3. add jdbc->kafka connector `http://localhost:8003/`
```
name=JdbcSourceConnector
connector.class=io.confluent.connect.jdbc.JdbcSourceConnector
tasks.max=1
connection.url=jdbc:postgresql://postgres/in
connection.user=postgres
connection.password=example
topic.prefix=inq
mode=incrementing
incrementing.column.name=id
```
4. check schema `http://localhost:8001`
5. check topic content `http://localhost:8000` (add/modify data)
6. `docker-compose -f docker-compose-fullstack.yaml exec ksqldb-server ksql`
 (or `docker run -it confluentinc/cp-ksqldb-cli http://localhost:8088`)
```
CREATE STREAM k WITH (
    kafka_topic = 'inqaccounts',
    value_format = 'avro'
);
SHOW STREAMS;

SELECT id, name FROM k EMIT CHANGES; # add record to postgres

CREATE TABLE support_view AS
    SELECT id, name FROM k EMIT CHANGES;

SHOW TABLES;

SHOW TOPICS;
PRINT 'inqaccounts' FROM BEGINNING;

SHOW CONNECTORS;
```


# References
* [bitnami kafka image](https://hub.docker.com/r/bitnami/kafka)
* [bitnami zookeeper image](https://hub.docker.com/r/bitnami/zookeeper)
* [Kafka Listeners - Explained](https://rmoff.net/2018/08/02/kafka-listeners-explained/)
* [Kafka listener vs advertised.listeners](https://stackoverflow.com/questions/42998859/kafka-server-configuration-listeners-vs-advertised-listeners#answer-43000344)
* [Kafkacat ](https://hub.docker.com/r/solsson/kafkacat)
* [Kafka connect avro jdbc](https://docs.confluent.io/5.0.0/installation/docker/docs/installation/connect-avro-jdbc.html)
* [Kafka source connector jdbc](https://docs.confluent.io/current/connect/kafka-connect-jdbc/source-connector/index.html#jdbc-source-configs-overview)
* [Kafka sink connector jdbc](https://docs.confluent.io/current/connect/kafka-connect-jdbc/sink-connector/index.html#connect-jdbc-sink)
* [Troubleshooting KSQL – Part 1: Why Isn’t My KSQL Query Returning Data?](https://www.confluent.io/blog/troubleshooting-ksql-part-1/)
* [Troubleshooting KSQL – Part 2: What’s Happening Under the Covers?](https://www.confluent.io/blog/troubleshooting-ksql-part-2/)
* [Ksql queries](https://docs.ksqldb.io/en/latest/concepts/queries/)