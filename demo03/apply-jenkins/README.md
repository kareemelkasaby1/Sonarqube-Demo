# Demo 03 - Apply Jenkins on K8S

There are multible resources needed to run `Jenkins` on K8S Cluster.

We are using [Docker Desktop](https://www.docker.com/products/docker-desktop/) as our K8S cluster provider.

[Jenkins Docker Hub](https://hub.docker.com/r/jenkins/jenkins)

## 1.1 Run Jenkins on K8S Steps:

> 1. Apply `Jenkins` resources:

```
kubectl apply -f jenkins
```
> 2. Go to slave and run:
```
service ssh start
passwd jenkins
--> 123456
```
> 4. Make sure everything is ok:
```
kubectl get all -n jenkins 

kubectl logs -f  -n jenkins -l app=jenkins
```
> 5. Go to jenkins GUI to do `Sonarqube configuration`:

Remember that the Sonarqube url must be `sonarqube.sonarqube:9000/sonar`.

`Go to` [Demo04](../../demo04/multi-branch-plugin/README.md)