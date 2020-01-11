# Query App Deployment

## Adding config map for query db and kafka

### Deploy query db confirm map

kubectl create -f querydb-configmap.yaml --namespace=project-logistics

### Deploy query db

kubectl create -f deploy-postgres-query.yaml --namespace=project-logistics

## Test Postgres connection

```
kubectl exec -it pod/logistics-query-db-65558c7987-tttt5 --namespace=project-logistics bash
psql -h localhost -U postgresadmin --password -p 5432 orderdemo_query
```

## build and push docker image for Query Service App

### run following command from project root folder

sudo docker build -t amitmahajan/logistics-query-api:0.1 .

sudo docker push amitmahajan/logistics-query-api:0.1

## Deploy query app

kubectl create -f deploy-query-app.yaml --namespace=project-logistics
