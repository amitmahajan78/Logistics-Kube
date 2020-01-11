# Deploy Auth Service

## Deploy auth service and create kube service

```
kubectl create -f deploy-auth.yaml --namespace=project-logistics
```

## Test Auth Service

curl --request POST --user server-server:server-server --url http://ae3459cd9331d11ea8a2306eb36976bd-1324349703.eu-west-2.elb.amazonaws.com:8090/oauth/token --header 'Content-Type: application/x-www-form-urlencoded' --data grant_type=client_credentials
