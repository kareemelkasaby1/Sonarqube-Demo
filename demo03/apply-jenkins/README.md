# Demo 03 - Apply Jenkins on K8S

There are multible resources needed to run `Jenkins` on K8S Cluster.

We are using [Docker Desktop](https://www.docker.com/products/docker-desktop/) as our K8S cluster provider.

[Jenkins Docker Hub](https://hub.docker.com/r/jenkins/jenkins)

## 1.1 Run Jenkins on K8S Steps:

> 1. Create Service Account:

```
kubectl create serviceaccount -n jenkins jenkins-deployer
```
> 2. Apply `Jenkins` resources:

```
kubectl apply -f jenkins
```
> 3. Create Cluster Role Binding:

```
kubectl create clusterrolebinding cluster-admin-jenkins-rolebinding  --clusterrole cluster-admin --serviceaccount jenkins:jenkins-deployer
```
> 4. Go to slave and run:
```
service ssh start
passwd jenkins
--> 123456
```
> 5. Make sure everything is ok:
```
kubectl get all -n jenkins 

kubectl logs -f  -n jenkins -l app=jenkins
```
> 6. Get kubeconfig of the service account:
```
kubectl config set-cluster cfc --server=https://kubernetes.default --certificate-authority=/var/run/secrets/kubernetes.io/serviceaccount/ca.crt

kubectl config set-context cfc --cluster=cfc

kubectl config set-credentials user --token=$(cat /var/run/secrets/kubernetes.io/serviceaccount/token)

kubectl config set-context cfc --user=user

kubectl config use-context cfc
```
> 7. Go to jenkins GUI to do `Sonarqube configuration`:

Remember that the Sonarqube url must be `sonarqube.sonarqube:9000/sonar`.

`Go to` [Demo04](../../demo04/multi-branch-plugin/README.md)