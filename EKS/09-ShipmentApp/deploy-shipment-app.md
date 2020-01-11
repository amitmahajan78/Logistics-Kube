# Shipment App Deployment

## build and push docker image for shipment Service App

### run following command from project root folder

sudo docker build -t amitmahajan/logistics-shipment-api:0.1 .

sudo docker push amitmahajan/logistics-shipment-api:0.1

## Deploy shipment app

kubectl create -f deploy-shipment-app.yaml --namespace=project-logistics
