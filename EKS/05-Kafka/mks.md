## Create a new kafka namespace for the Strimzi Kafka Cluster Operator.

kubectl create ns kafka
kubectl apply -f strimzi-0.16.2/install/cluster-operator/ -n kafka
kubectl apply -f strimzi-0.16.2/install/cluster-operator/020-RoleBinding-strimzi-cluster-operator.yaml -n project-logistics
kubectl apply -f strimzi-0.16.2/install/cluster-operator/032-RoleBinding-strimzi-cluster-operator-topic-operator-delegation.yaml -n project-logistics
kubectl apply -f strimzi-0.16.2/install/cluster-operator/031-RoleBinding-strimzi-cluster-operator-entity-operator-delegation.yaml -n project-logistics
watch kubectl get all --namespace=kafka

## With Strimzi installed, you create a Kafka cluster, then a topic within the cluster.

kubectl create -f kafka-cluster.Kafka.yaml --namespace=project-logistics
kubectl wait kafka/kafka-cluster --for=condition=Ready --timeout=300s -n project-logistics

kubectl get statefulsets.apps,pod,deployments,svc --namespace=project-logistics

kubectl apply -f create-topics.yaml --namespace=project-logistics
kubectl create -f kafka-host-configmap.yaml --namespace=project-logistics












# Create the configmap, which contains details such as the broker DNS names, topic name and consumer group ID

kubectl apply -f test/k8s/config.yaml --namespace=project-logistics

# Create the producer deployment

kubectl apply -f test/k8s/producer.Deployment.yaml --namespace=project-logistics

# Expose the producer deployment via a service of type LoadBalancer (backed by the AWS Elastic Load Balancer). This just makes it easy for me to curl from postman

kubectl apply -f test/k8s/producer.Service.yaml --namespace=project-logistics

# Finally, create the consumer deployment

kubectl apply -f test/k8s/consumer.Deployment.yaml --namespace=project-logistics

kubectl get svc --namespace=project-logistics

kubectl get pod --namespace=project-logistics

# Delete the test producer and consumer apps:

kubectl delete -f test/k8s/
configmap "kafka-client-config" deleted
deployment.apps "node-test-consumer" deleted
deployment.apps "node-test-producer" deleted
service "node-test-producer" deleted

# Delete the Strimzi cluster operator

kubectl delete deployments. strimzi-cluster-operator --namespace=project-logistics
deployment.extensions "strimzi-cluster-operator" deleted

# Manually delete the persistent volumes

# Kafka

kubectl delete pvc data-kafka-cluster-kafka-0 --namespace=project-logistics
kubectl delete pvc data-kafka-cluster-kafka-1 --namespace=project-logistics
kubectl delete pvc data-kafka-cluster-kafka-2 --namespace=project-logistics

# Zookeeper

kubectl delete pvc data-kafka-cluster-zookeeper-0 --namespace=project-logistics
kubectl delete pvc data-kafka-cluster-zookeeper-1 --namespace=project-logistics
kubectl delete pvc data-kafka-cluster-zookeeper-2 --namespace=project-logistics
