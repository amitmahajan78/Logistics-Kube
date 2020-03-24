# Gateway App Deployment

## build and push docker image for gateway Service App

### run following command from project root folder

sudo docker build -t amitmahajan/gateway:0.1 .

sudo docker push amitmahajan/gateway:0.1

## Deploy shipment app

kubectl create -f deploy-gateway-app.yaml --namespace=project-logistics
