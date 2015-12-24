```bash
# create a service, pod, or replication controller
kubectl create -f <json or yaml file>

# get stream of kubernetes events
kubectl get events --watch-only

# scale up and down replication controller pods
kubectl scale rc <replication controller name> --replicas=0; kubectl scale rc <replication controller name> --replicas=2;

```
