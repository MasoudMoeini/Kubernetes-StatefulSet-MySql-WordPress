# Kubernetes StatefulSet MySql WordPress
Deploying WordPress and MySQL with Persistent Volumes [Reference](https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/) <br>
This web application uses Wordpress as a Frontend and MySql database as backend<br>
Apple Silicon (M1, etc.) or a Raspberry Pi, which are both arm64 based processors,<br>
does not support MySql Alternative change  **mysql to mariadb**   and everything should work.<br>
Both applications use PersistentVolumes and PersistentVolumeClaims to store data.<br>
Create kustomization.yaml and add secrect for password <br>
```
cat <<EOF >./kustomization.yaml
secretGenerator:
- name: mysql-pass
  literals:
  - password={YOUR_PASSWORD}
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
If all pods are running, to access the wordpredd web application via ingress 
```
kubectl get services wordpress
```
```
kubectl apply -f wordpress-ingress.yaml
```
```
kubectl get ingress
```
Update /etc/hosts file with "127.0.0.1 wordpress-app-host.info" at the last line [Instruction](https://help.nexcess.net/en_US/miscellaneous/how-to-find-the-hosts-file-on-my-mac)
```
http://wordpress-app-host.info 
```
Now you should see on browser <br>
If pods are not running test mysql image on your system <br>
```
docker pull --platform linux/x86_64 mysql
docker run --platform linux/x86_64 mysql:5.7 -e MYSQL_ROOT_PASSWORD=pass
```
If mysql image is not working use mariadb-deployment.yaml for deployment 
To Delete all resources 
```
kubectl delete -k ./
```
# MariaDb WordPress
Test mariadb image
```
docker run -d -p 3306:3306 --name db -e MYSQL_ROOT_PASSWORD=mypass mariadb
``` 
```
cat <<EOF >>./kustomization.yaml
resources:
  - mariadb-deployment.yaml
  - wordpress-deployment.yaml
EOF
```
