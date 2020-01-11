# create namespace

```
kubectl create namespace project-logistics
```

# create storage and RBAC

The corresponding commands are:

```
kubectl apply -f create-rbac.yaml --namespace=project-logistics
kubectl apply -f create-efs-provisioner.yaml --namespace=project-logistics
```
