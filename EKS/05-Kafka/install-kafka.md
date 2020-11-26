
sed -i '' 's/namespace: .*/namespace: kafka-operator/' install/cluster-operator/*RoleBinding*.yaml

kubectl create ns kafka-apps

kubectl apply -f install/cluster-operator/020-RoleBinding-strimzi-cluster-operator.yaml -n kafka-apps
kubectl apply -f install/cluster-operator/031-RoleBinding-strimzi-cluster-operator-entity-operator-delegation.yaml -n kafka-apps
kubectl apply -f install/cluster-operator/032-RoleBinding-strimzi-cluster-operator-topic-operator-delegation.yaml -n kafka-apps


kubectl apply -f install/cluster-operator -n kafka-operator

kubectl get deployments -n kafka

kubectl apply -f kafka-persistent.yaml -n kafka-apps

kubectl get statefulsets.apps,pod,deployments,svc --namespace=kafka-apps


kubectl -n kafka-apps run kafka-producer -ti --image=strimzi/kafka:0.19.0-kafka-2.5.0 --rm=true --restart=Never -- bin/kafka-console-producer.sh --broker-list kafka-cluster-kafka-bootstrap:9092 --topic my-topic


kubectl -n kafka-apps run kafka-consumer -ti --image=strimzi/kafka:0.19.0-kafka-2.5.0 --rm=true --restart=Never -- bin/kafka-console-consumer.sh --bootstrap-server kafka-cluster-kafka-bootstrap:9092 --topic my-topic --from-beginning


kubectl apply -f kafka-persistent.yaml -n kafka-apps



curl -s https://raw.githubusercontent.com/coreos/prometheus-operator/master/bundle.yaml > prometheus-operator-deployment.yaml


sed -i '' 's/namespace: .*/namespace: metrics-operator/' prometheus-operator-deployment.yaml

kubectl apply -f prometheus-operator-deployment.yaml -n metrics-operator

sed -i '' 's/namespace: .*/namespace: metrics-operator/' examples/metrics/prometheus-install/prometheus.yaml


kubectl create secret generic additional-scrape-configs --from-file=examples/metrics/prometheus-install/prometheus-additional.yaml -n metrics-operator


kubectl apply -f examples/metrics/prometheus-install/strimzi-pod-monitor.yaml -n metrics-operator
kubectl apply -f examples/metrics/prometheus-install/prometheus-rules.yaml -n metrics-operator
kubectl apply -f examples/metrics/prometheus-install/prometheus.yaml -n metrics-operator


kubectl apply -f examples/metrics/grafana-install/grafana.yaml -n metrics-operator

kubectl get service grafana -n metrics-operator


kubectl apply -f examples/topic/kafka-topic.yaml -n kafka-apps