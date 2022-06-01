# Demo 04 - Install Multi-Branch Plugin: 

We just need simple modifications to install the third party multi branch pipeline.

We are using [Docker Desktop](https://www.docker.com/products/docker-desktop/) as our K8S cluster provider.

[Plugin Github](https://github.com/mc1arke/sonarqube-community-branch-plugin)
## 1.1 Run Sonarqube with the third party plugin configuration:
> 1. Download the plugin Jar:
```
wget https://github.com/mc1arke/sonarqube-community-branch-plugin/releases/download/1.8.0/sonarqube-community-branch-plugin-1.8.0.jar -O ../../demo02/apply-sonarqube/sonarqube-extensions/plugins/sonarqube-community-branch-plugin-1.8.0.jar
```

> 2. Apply [Sonarqube Deployment](sonarqube-deploy-with-multibranch-plugin.yml) again with the changes:
```
kubectl apply -f sonarqube-deploy-with-multibranch-plugin.yml
```
> 3. Make sure everything is ok:
```
kubectl get all -n sonarqube 

kubectl logs -f  -n sonarqube -l name=sonarqube
```