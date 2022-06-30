# Kubernetes StatefulSet MySql WordPress
Deploying WordPress and MySQL with Persistent Volumes [Reference](https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/) <br>
This web application uses Wordpress as a Frontend and MySql database as backend<br>
Apple Silicon (M1, etc.) or a Raspberry Pi, which are both arm64 based processors,does not support MySql<br>
Alternative change  **mysql to mariadb**   and everything should work<br>
Both applications use PersistentVolumes and PersistentVolumeClaims to store data.<br>
Create kustomization.yaml and add secrect for assets or credential 
```
cat <<EOF >./kustomization.yaml
secretGenerator:
- name: mysql-pass
  literals:
  - password={YOUR_PASSWORD}
EOF
```
```
cat <<EOF >>./kustomization.yaml
resources:
  - mysql-deployment.yaml
  - wordpress-deployment.yaml
EOF
```
Adding both wordpress-deployment.yaml and msql-deployment.yaml to kustomization.yaml
```
cat <<EOF >>./kustomization.yaml
resources:
  - mysql-deployment.yaml
  - wordpress-deployment.yaml
EOF
```
```
kubectl apply -k ./
```
Now all the resources has been created
```
kubectl get secrets
kubectl get pvc
kubectl get pods
``` 
If all pods are running
```
kubectl get services wordpress
curl http://localhost:80
```
Exceptions
```
docker pull --platform linux/x86_64 mysql
docker run --platform linux/x86_64 mysql:5.7 -e MYSQL_ROOT_PASSWORD=pass
```
To Delete all resources 
```
kubectl delete -k ./
```