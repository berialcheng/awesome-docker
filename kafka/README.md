

# Get started
0. `docker-compose up -d`
1. 
    ```
    docker run -it --rm \
    --network kafka_default \
    -e KAFKA_CFG_ZOOKEEPER_CONNECT=zookeeper:2181 \
    bitnami/kafka:latest kafka-topics.sh --list  --zookeeper zookeeper:2181
    ```
2. ```
docker run -it --rm \
    --network kafka_default \
    -e KAFKA_CFG_ZOOKEEPER_CONNECT=zookeeper:2181 \
    bitnami/kafka:latest bash
```
    *  
    * 

# 
* [bitnami kafka image](https://hub.docker.com/r/bitnami/kafka)
* [bitnami zookeeper image](https://hub.docker.com/r/bitnami/zookeeper)
* [Kafka Listeners - Explained](https://rmoff.net/2018/08/02/kafka-listeners-explained/)
