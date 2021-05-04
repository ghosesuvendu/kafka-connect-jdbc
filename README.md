# kafka-connect-jdbc
This repository shows docker-compose based Kafka JDBC connector configuration for postgres DB

Below are the steps, need to perform as prerequisite, as I am configuring this in a way so that Plug_in Jars will be taken only from the physical directory as offline mode (not as online mode).

1.	docker pull confluentinc/cp-kafka-connect
2.	docker pull confluentinc/cp-zookeeper
3.	docker pull confluentinc/cp-kafka
4.	download kafka-connect jdbc zip from the below link, unzip and save all plugin jars under a directory, (for example here I am using path ‘/home/dmprojects/kafka-connect/vol42/kafka-connect/jars’)
https://www.confluent.io/hub/confluentinc/kafka-connect-jdbc

