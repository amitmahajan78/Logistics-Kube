## Installing Helm

I use Homebrew, so the installation was pretty straightforward: brew install kubernetes-helm.

Alternatively, to install helm, run the following:
\$ cd ~/eks-kafka-strimzi

\$ curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get > get_helm.sh

\$ chmod +x get_helm.sh

\$ ./get_helm.sh

## Setup and deploy kafka operator

kubectl apply -f rbac.yaml --namespace=project-logistics
helm init --service-account=tiller
helm repo add strimzi http://strimzi.io/charts/
helm search strim
helm install strimzi/strimzi-kafka-operator --namespace=project-logistics
kubectl get all --namespace=project-logistics
kubectl apply -f kafka-cluster.Kafka.yaml --namespace=project-logistics
kubectl get statefulsets.apps,pod,deployments,svc --namespace=project-logistics
kubectl get pv,pvc --namespace=project-logistics
kubectl apply -f create-topics.yaml --namespace=project-logistics

### deploy kafka host config

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

kubectl delete deployments. strimzi-cluster-operator
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
