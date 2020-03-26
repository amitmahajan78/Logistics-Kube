# Deploy Retail app

## Deploy retail bff (backend) app

kubectl create -f deploy-retail-bff-app.yaml --namespace=project-logistics

## Deploy retail app

## Before we deploy retail-app, we need to get the EXTERNAL-IP for retail-bff-app and update the deploy-retail-app.yaml file with the value.

kubectl create -f deploy-retail-app.yaml --namespace=project-logistics
