**Kafka Initialization Guide**

Kafka keeps a track of all the topics ,and consumer groups self balancing -> Zookeeper

![image](https://github.com/user-attachments/assets/046ac7d4-65fd-4691-90ab-e8494380ce19)




We have to set a zookeeper service running on some port, so that the kafka system can interact with it



```docker run -p 2181:2181 zookeeper```


2181 is zookeper’s default port, by running this command, it acquires zookeeper image from docker hub (It’ll first be unable to find it locally, that’s totally normal)


- Next we run kafka, to run kafka ,it usually uses port 9092, we can stick with that itself


Some details needed for kafka to run:


- It should know where to find the zookeeper running ,ex: if on 2181 then its exact location would be 192.169.0.103:2181 (where 192.169.0.103 is your private IP you can find in your wifi settings on your device)
- We should also tell kafka which is the port where we will listen to it, aka which port it will be run on, ex: 192.169.0.103:9092 (if you’re running it on 9092 port)
- Number of topic replications (usually 1 , similar to database replications)


The docker command to run kafka is this:


```docker run -p 9092:9092 --env KAFKA_ZOOKEEPER_CONNECT=192.168.0.103:2181 --env KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://192.168.0.103:9092 --env KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR=1 confluentinc/cp-kafka```

Where confluentinc/cp-kafka is kafka image on docker hub

Different roles can set up different parts of kafka architecture:

1. Admin: sets up kafka infra, like topics ,partitions

- The entire service running on say 9092 is called a broker

1. Producer: produces messages
2. Consumer: consumes messages from topics

Refer kafka js documentation at <https://kafka.js.org/docs/consuming> to learn how to setup your workflow with Kafka services using Express!
