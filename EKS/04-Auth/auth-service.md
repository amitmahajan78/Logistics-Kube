# Deploy Auth Service

## Deploy auth service and create kube service

```
kubectl create -f deploy-auth.yaml --namespace=project-logistics
```

## Test Auth Service

curl --request POST --user server-server:server-server --url http:/logistics-auth-service:8090/oauth/token --header 'Content-Type: application/x-www-form-urlencoded' --data grant_type=client_credentials
