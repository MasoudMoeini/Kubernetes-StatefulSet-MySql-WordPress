# Deploying Cassandra with a StatefulSet
[Reference](https://kubernetes.io/docs/tutorials/stateful-application/cassandra/)
```
kubectl apply -f cassandra-service.yaml
```
```
kubectl get svc cassandra
```
Using a StatefulSet to create a Cassandra ring
```
cassandra-statefulset.yaml
```
Validating the Cassandra StatefulSet
```
kubectl get statefulset cassandra
kubectl get pods -l="app=cassandra"
```
Run the Cassandra nodetool inside the first Pod, to display the status of the ring
```
kubectl exec -it cassandra-0 -- nodetool status
```
Modifying StatefulSet
```
kubectl edit statefulset cassandra
```
Change the number of replicas to 4
```
kubectl get statefulset cassandra
```
Deleting Resources 
```
  kubectl delete service -l app=cassandra\
  && kubectl delete statefulset -l app=cassandra \
  && kubectl delete persistentvolumeclaim -l app=cassandra
```
```
kubectl delete service -l app=cassandra
```

