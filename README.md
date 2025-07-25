# hello-kafka
A simple guide to install, configure, and use Apache Kafka (topics, producers, consumers, etc.)

## 📦 Installation

Kafka requires Java. You can install OpenJDK:
```bash
sudo apt update
sudo apt install default-jdk -y
java -version
```


### Download and Extract Kafka 2.13-3.4.0

Connect to the server as root directly, or through sudo:
`sudo -i`

Create kafka user :
`useradd kafka`

Grant permissions to the kafka user on the directory:
`chown kafka:kafka kafka_2.13-3.4.0/ -R`

```bash
cd /opt
wget https://downloads.apache.org/kafka/3.7.0/kafka_2.13-3.4.0.tgz
tar -xzf kafka_2.13-3.4.0.tgz
rm kafka_2.13-3.4.0.tgz
ln -s kafka_2.13-3.4.0 kafka
```
## ⚙️ Configuration
### Set Up Kafka as a Service

Copy kafka-zookeeper.service in `/etc/systemd/system/kafka-zookeeper.service`

Copy kafka.service dans in `/etc/systemd/system/kafka.service`

### Enable and start the Kafka/zookeeper service:

Enable and start services:
```bash
sudo systemctl enable kafka-zookeeper.service
sudo systemctl start kafka-zookeeper.service
sudo systemctl enable kafka.service
sudo systemctl start kafka.service
```

Check that the services have started correctly:
```bash
systemctl status kafka-zookeeper  
systemctl status kafka
```

## 🧵 Kafka Topics
### Create a Topic
```bash
bin/kafka-topics.sh --create --topic YOUR_TOPIC_NAME --bootstrap-server localhost:9092
```

### List Topics
```bash
bin/kafka-topics.sh --bootstrap-server localhost:9092 --list
```

### Delete a Topic
```bash
bin/kafka-topics.sh --bootstrap-server localhost:9092 --delete --topic YOUR_TOPIC_NAME
```

## ✍️ Producers & Consumers
### Write Events (Producer)
```bash
bin/kafka-console-producer.sh --topic YOUR_TOPIC_NAME --bootstrap-server localhost:9092
```

### Read Events (Consumer)
```bash
bin/kafka-console-consumer.sh --topic YOUR_TOPIC_NAME --from-beginning --bootstrap-server localhost:9092
```

## 🖥 Kafka UI (Optional)
```bash
sudo docker run -d --name kafka-ui -p 8080:8080 \
-e KAFKA_CLUSTERS_0_NAME=local \
-e KAFKA_CLUSTERS_0_BOOTSTRAPSERVERS=localhost:9092 \
provectuslabs/kafka-ui:latest
```