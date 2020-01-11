# Stock App Deployment

## Adding config map for stock db and kafka

### Deploy stock db confirm map

kubectl create -f stockdb-configmap.yaml --namespace=project-logistics

### Deploy stock db

kubectl create -f deploy-postgres-stock.yaml --namespace=project-logistics

## Test Postgres connection

```
kubectl exec -it pod/logistics-stock-db-5f45584d7-gp5mn --namespace=project-logistics bash
psql -h localhost -U postgresadmin --password -p 5432 stock_db
```

## build and push docker image for stock Service App

### run following command from project root folder

sudo docker build -t amitmahajan/logistics-stock-api:0.1 .

sudo docker push amitmahajan/logistics-stock-api:0.1

## Deploy stock app

kubectl create -f deploy-stock-app.yaml --namespace=project-logistics
