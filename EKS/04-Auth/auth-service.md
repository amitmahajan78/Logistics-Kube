# Deploy Auth Service

## Deploy auth service and create kube service

```
kubectl create -f deploy-auth.yaml --namespace=project-logistics
```

## Test Auth Service

curl --request POST --user server-server:server-server --url http://a5d96584d771311ea99a102ab2b0033e-222267424.eu-west-2.elb.amazonaws.com:9090/oauth/token --header 'Content-Type: application/x-www-form-urlencoded' --data grant_type=client_credentials
