# Deploy Auth Service

## Deploy auth service and create kube service

```
kubectl create -f deploy-auth.yaml --namespace=project-logistics
```

## Test Auth Service

curl --request POST --user server-server:server-server --url http://ab0eeff656de311eaab5802c43b171f6-1286383641.eu-west-2.elb.amazonaws.com:8090/oauth/token --header 'Content-Type: application/x-www-form-urlencoded' --data grant_type=client_credentials
