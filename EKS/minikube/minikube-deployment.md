
## Installing Istio
kubectl apply -f 1-istio-init.yaml
kubectl apply -f 2-istio-minikube.yaml
watch kubectl get po -n istio-system

kubectl apply -f 3-kiali-secret.yaml

## Logistics Namespace

kubectl create namespace project-logistics
kubectl label namespace project-logistics istio-injection=enabled
kubectl get namespace -L istio-injection

## Kafka deployment .. goto kafka folder 05-Kafka and run the scripts from there

## Logistics PV, PVC

## Run only for EFS on AWS EKS
kubectl apply -f ../02-EFS/create-rbac.yaml --namespace=project-logistics
kubectl apply -f ../02-EFS/create-efs-provisioner.yaml --namespace=project-logistics
kubectl create -f ../03-PostgreSQL/create-storage.yaml --namespace=project-logistics

## Run only for locl minikube
kubectl create -f ../03-PostgreSQL/persistent-volumes-minikube.yml --namespace=project-logistics
kubectl get pv,pvc -n project-logistics

## Config Maps 

kubectl create -f ../03-PostgreSQL/authdb-configmap.yaml --namespace=project-logistics
kubectl create -f ../06-OrderApp/orderdb-configmap.yaml --namespace=project-logistics
kubectl create -f ../07-QueryApp/querydb-configmap.yaml --namespace=project-logistics
kubectl create -f ../08-StockApp/stockdb-configmap.yaml --namespace=project-logistics


## Databases

kubectl create -f ../03-PostgreSQL/deploy-postgres-auth.yaml --namespace=project-logistics
kubectl create -f ../06-OrderApp/deploy-postgres-order.yaml --namespace=project-logistics
kubectl create -f ../07-QueryApp/deploy-postgres-query.yaml --namespace=project-logistics
kubectl create -f ../08-StockApp/deploy-postgres-stock.yaml --namespace=project-logistics
watch kubectl get svc,po -n project-logistics

## Services

kubectl create -f ../04-Auth/deploy-auth.yaml --namespace=project-logistics
kubectl create -f ../10-Gateway/deploy-gateway-app.yaml --namespace=project-logistics
kubectl create -f ../06-OrderApp/deploy-order-app.yaml --namespace=project-logistics
kubectl create -f ../07-QueryApp/deploy-query-app.yaml --namespace=project-logistics
kubectl create -f ../08-StockApp/deploy-stock-app.yaml --namespace=project-logistics
kubectl create -f ../09-ShipmentApp/deploy-shipment-app.yaml --namespace=project-logistics
watch kubectl get svc,po -n project-logistics


## SupplyChain

kubectl create -f ../11-SupplyChainApp/supplychaindb-configmap.yaml --namespace=project-logistics

kubectl create -f ../11-SupplyChainApp/deploy-postgres-supplychain.yaml --namespace=project-logistics

watch kubectl get svc,po -n project-logistics

```
kubectl exec -it logistics-supplychain-db-7bfcdc88b5-ljdct --namespace=project-logistics bash
psql -h localhost -U orderdemo --password -p 5432 supplychain_db
```

PSQL Commands: https://www.postgresqltutorial.com/psql-commands/

CREATE TABLE shedlock(
name VARCHAR(64),
lock_until TIMESTAMP(3) NULL,
locked_at TIMESTAMP(3) NULL,
locked_by VARCHAR(255),
PRIMARY KEY (name)
);

kubectl create -f ../11-SupplyChainApp/deploy-supplychain-app.yaml --namespace=project-logistics
watch kubectl get svc,po -n project-logistics


## Retail

kubectl create -f ../12-RetailApp/deploy-retail-bff-app.yaml --namespace=project-logistics

kubectl create -f ../12-RetailApp/deploy-retail-app.yaml --namespace=project-logistics

