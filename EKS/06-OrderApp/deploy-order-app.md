# Order App Deployment

## Adding config map for order db and kafka

### Deploy order db confirm map

kubectl create -f querydb-configmap.yaml --namespace=project-logistics

### Deploy order db

kubectl create -f deploy-postgres-order.yaml --namespace=project-logistics

## Test Postgres connection

```
kubectl exec -it pod/logistics-order-db-65b4c78555-krkp5 --namespace=project-logistics bash
psql -h localhost -U postgresadmin --password -p 5432 orderdemo_cmd
```

### deploy kafka host config

kubectl create -f kafka-host-configmap.yaml --namespace=project-logistics

## Deploy kafka topic

kubectl create -f create-topics.yaml --namespace=project-logistics

## build and push docker image for Order Service App

### run following command from project root folder

sudo docker build -t amitmahajan/logistics-order-api:0.1 .

sudo docker push amitmahajan/logistics-order-api:0.1

## Deploy order app

kubectl create -f deploy-order-app.yaml --namespace=project-logistics
