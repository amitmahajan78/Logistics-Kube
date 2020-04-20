# supplychain App Deployment

## Adding config map for supplychain db and kafka

### Deploy supplychain db confirm map

kubectl create -f supplychaindb-configmap.yaml --namespace=project-logistics

### Deploy supplychain db

kubectl create -f deploy-postgres-supplychain.yaml --namespace=project-logistics

## Test Postgres connection and create shedlock table

```
kubectl exec -it logistics-supplychain-db-86b55ccf9f-8gwx7 --namespace=project-logistics bash
psql -h localhost -U orderdemo --password -p 5432 supplychain_db
```

PSQL Commands: https://www.postgresqltutorial.com/psql-commands/

### create following table

CREATE TABLE shedlock(
name VARCHAR(64),
lock_until TIMESTAMP(3) NULL,
locked_at TIMESTAMP(3) NULL,
locked_by VARCHAR(255),
PRIMARY KEY (name)
);

## Deploy supplychain app

kubectl create -f deploy-supplychain-app.yaml --namespace=project-logistics
