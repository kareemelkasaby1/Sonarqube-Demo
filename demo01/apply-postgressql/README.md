# Demo 01 - Apply Postgress on K8S

There are multible resources needed to run `Postgress` on K8S Cluster.

We are using [Docker Desktop](https://www.docker.com/products/docker-desktop/) as our K8S cluster provider.

[Postgress Docker Hub](https://hub.docker.com/_/postgres)

## 1.1 Run Postgress on K8S Steps:

> 1. Create [Sonarqube namspace](sonarqube-namespace.yml):

```
kubectl apply -f sonarqube-namespace.yml
```
> 2. Create [Pstgress PV](postgress-pv.yml):

```
kubectl apply -f postgress-pv.yml
```
> 3. Create [Pstgress PVC](postgress-pvc.yml):
```
kubectl apply -f postgress-pvc.yml
```
> 4. Create [Pstgress Service](postgress-svc.yml):

```
kubectl apply -f postgress-svc.yml
```
> 5. Create [Pstgress Deploy](postgress-deploy.yml):
```
kubectl apply -f postgress-deploy.yml
```
> 6. Make sure everything is ok:
```
kubectl get all -n sonarqube 

kubectl logs -f  -n sonarqube -l name=sonar-postgres
```
`Go to` [Demo02](../../demo02/apply-sonarqube/README.md)