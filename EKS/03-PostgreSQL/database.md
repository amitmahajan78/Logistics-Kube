# Deploy postgres

## Create config map

```
kubectl create -f authdb-configmap.yaml --namespace=project-logistics
```

## Create storage (storage class and persistence volume claim)

```
kubectl create -f create-storage.yaml --namespace=project-logistics
```

## Deploy postgres database and create service

```
kubectl create -f deploy-postgres-auth.yaml --namespace=project-logistics
```

## Test Postgres connection

```
kubectl exec -it logistics-auth-db-764ffcb695-9rqbs --namespace=project-logistics bash
psql -h localhost -U postgresadmin --password -p 5432 auth_server
```
