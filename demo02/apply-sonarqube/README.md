# Demo 02 - Apply Sonarqube on K8S

There are multible resources needed to run `Sonarqube` on K8S Cluster.

We are using [Docker Desktop](https://www.docker.com/products/docker-desktop/) as our K8S cluster provider.

[Sonarqube Docker Hub](https://hub.docker.com/_/sonarqube)

## 1.1 Run Postgress on K8S Steps:

> 1. Create [Sonarqube Extensions PV](sonarqube-extensions-pv.yml):

```
kubectl apply -f sonarqube-extensions-pv.yml
```
> 2. Create [Sonarqube Extensions PVC](sonarqube-extensions-pvc.yml):
```
kubectl apply -f sonarqube-extensions-pvc.yml
```
> 3. Create [Sonarqube logs PV](sonarqube-logs-pv.yml):

```
kubectl apply -f sonarqube-logs-pv.yml
```
> 4. Create [Sonarqube Logs PVC](sonarqube-logs-pvc.yml):
```
kubectl apply -f sonarqube-logs-pvc.yml
```
> 5. Create [Sonarqube Conf PV](sonarqube-conf-pv.yml):

```
kubectl apply -f sonarqube-conf-pv.yml
```
> 6. Create [Sonarqube Conf PVC](sonarqube-conf-pvc.yml):
```
kubectl apply -f sonarqube-conf-pvc.yml
```
> 7. Create [Sonarqube Data PV](sonarqube-data-pv.yml):

```
kubectl apply -f sonarqube-data-pv.yml
```
> 8. Create [Sonarqube Data PVC](sonarqube-data-pvc.yml):
```
kubectl apply -f sonarqube-data-pvc.yml
```
> 9. Create [Sonarqube Service](sonarqube-svc.yml):
```
kubectl apply -f sonarqube-svc.yml
```
> 10. Create [Sonarqube Deployment]( sonarqube-deploy-without-multibranch.yml):
```
kubectl apply -f  sonarqube-deploy-without-multibranch.yml
```
> 11. Add another host of sonar.local.com in `/etc/hosts`:
```
vi /etc/hosts

127.0.0.1       sonar.local.com
```
> 11. Create [Sonarqube Ingress](sonarqube-ingress.yml):
```
kubectl apply -f sonarqube-ingress.yml
```
> 12. Install [ingress controller](https://kubernetes.github.io/ingress-nginx/deploy/#docker-for-mac) to Docker Desktop:
```
helm upgrade --install ingress-nginx ingress-nginx \
  --repo https://kubernetes.github.io/ingress-nginx \
  --namespace ingress-nginx --create-namespace
```
> 13. Forward `8080` to `80` inside K8S cluster:
```
kubectl port-forward --namespace=ingress-nginx service/ingress-nginx-controller 8080:80 
```
> 14. Make sure everything is ok:
```
kubectl get all -n sonarqube 

kubectl logs -f  -n sonarqube -l name=sonarqube
```

`Go to` [Demo03](../../demo03/apply-jenkins/README.md)