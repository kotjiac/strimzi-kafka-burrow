# References

* Run Kafka on Kubernetes:
https://github.com/strimzi/strimzi-kafka-operator

* Kafka Consumer Lag Monitoring:
https://github.com/linkedin/Burrow

* Run Kubernetes Made Simple:
https://k3s.io

# First Things First

## Install All You Need

K3S

```bash
curl -sfL https://get.k3s.io | sh -
```

Strimzi Kafka Operator

```bash
kubectl create ns kafka-operator
helm install strimzi-cluster-operator oci://quay.io/strimzi-helm/strimzi-kafka-operator -n kafka-operator
```

## Create Kafka Cluster

```bash
kubectl create ns kafka-cluster
kubectl apply -f kafka-cluster/ -n kafka-cluster
```

## Build Burrow Docker Image

```bash
cd burrow/Linkedin-Burrow
docker build -t your-registry/your-image:your-tag .
```

## Create Burrow Deployment

```bash
kubectl apply -f burrow/manifests/ -n kafka-cluster
```

# Testing

* Port-Forward Kafka Services
* Install kafkacat
* Produce messages

```bash
echo "hello from kafkacat" | kafkacat -P -t [TOPIC_NAME] -b [KAFKA_HOST:KAFKA_PORT] -X security.protocol=SASL_SSL -X sasl.mechanisms=SCRAM-SHA-512 -X sasl.username=kafka-burrow -X sasl.password=[PASSWORD]
```

* Consume messages

```bash
kafkacat -C -t [TOPIC_NAME] -b [KAFKA_HOST:KAFKA_PORT] -X security.protocol=SASL_SSL -X sasl.mechanisms=SCRAM-SHA-512 -X sasl.username=kafka-burrow -X sasl.password=[PASSWORD]
```