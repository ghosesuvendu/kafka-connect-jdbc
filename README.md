# kafka-connect-jdbc
This repository shows docker-compose based Kafka JDBC connector configuration for postgres DB

Below are the steps, need to perform as prerequisite, as I am configuring this in a way so that Plug_in Jars will be taken only from the physical directory as offline mode (not as online mode).

1.	docker pull confluentinc/cp-kafka-connect
2.	docker pull confluentinc/cp-zookeeper
3.	docker pull confluentinc/cp-kafka
4.	download kafka-connect jdbc zip from the below link, unzip and save all plugin jars under a directory, (for example here I am using path ‘/home/dmprojects/kafka-connect/vol42/kafka-connect/jars’)
https://www.confluent.io/hub/confluentinc/kafka-connect-jdbc

**Source connector Configurations:**

curl -X POST http://10.129.174.174:8082/connectors -H "Content-Type: application/json" -d '{
        "name": "jdbc_source_postgres_04",
        "config": {
                "connector.class": "io.confluent.connect.jdbc.JdbcSourceConnector",
                  "connection.url": "jdbc:postgresql://10.129.174.174:5432/postgres",
                "connection.user": "postgres",
                "connection.password": "postgres",
                "topic.prefix": "postgres-02-",
                "mode":"bulk",
                "poll.interval.ms": 3600000
                }
        }'

**Sink connector Configurations:**

curl -X POST http://10.129.174.174:8082/connectors -H "Content-Type: application/json" -d '{
        "name": "jdbc_sink_postgres_04",
        "config": {
                "connector.class": "io.confluent.connect.jdbc.JdbcSinkConnector",
                  "connection.url": "jdbc:postgresql://10.129.174.174:5432/postgres",
                "connection.user": "postgres",
                "connection.password": "postgres",
                "topics": "postgres-02-Test1",
                "auto.create": "true",
                "insert.mode":"insert",
                "table.name.format": "Test4",
                "mode":"bulk",
                "pk.mode":"none",
                "poll.interval.ms": 60000,
                "pk.mofr":"bulk"
                }
}'
