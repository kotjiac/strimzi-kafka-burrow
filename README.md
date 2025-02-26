# References

## Run Kafka on Kubernetes
https://github.com/strimzi/strimzi-kafka-operator

## Kafka Consumer Lag Monitoring
https://github.com/linkedin/Burrow

## Run Kubernetes Made Simple
https://k3s.io

# First Things First

## Install All You Need

### K3S

```bash
curl -sfL https://get.k3s.io | sh -
```

### Strimzi Kafka Operator

```bash
helm install strimzi-cluster-operator oci://quay.io/strimzi-helm/strimzi-kafka-operator
```

## Create Kafka Cluster

## Create Burrow Deployment