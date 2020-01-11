# use eksctl to create EKS cluster

display available options and properties:

```bash
eksctl create cluster --help
```

## creation

create cluster by using yaml config file:

```bash
eksctl create cluster -f eks-logistics.yaml
```

## post-install check

eksctl also creates the config file for _kubectl_. This means we can immediately fire up a check like:

```
kubectl get nodes
```

## delete a nodegroup

```bash
eksctl delete nodegroup --cluster=EKS-cluster --name=ng-group-mixed
```

or

```bash
eksctl delete nodegroup --config-file=eks-course.yaml --include=ng-mixed --approve
```

## delete cluster

```bash
eksctl delete cluster -f eks-logistics.yaml
```
