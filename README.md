# Kubernetes StatefulSet MySql WordPress
Deploying WordPress and MySQL with Persistent Volumes [Reference](https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/) <br>


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
To Delete all resources 
```
kubectl delete -k ./
```

