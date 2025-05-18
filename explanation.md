

## Explanation of Architecture

### 1. Kubernetes Object Choices

* MongoDB is deployed as a StatefulSet with a persistent volume.
* Frontend and backend are deployed using Deployments since they are stateless.

### 2. Exposure

* The frontend is exposed via a NodePort service using minikube service.
* Backend and MongoDB are ClusterIP services for internal communication.

### 3. Persistent Storage

* MongoDB uses a PVC backed by hostPath storage in Minikube for data persistence.



## Testing and Debugging


* View services

kubectl get services

* View running pods:

kubectl get pods


* View logs:

kubectl logs <pod-name>


* Enter a container:

kubectl exec -it <pod-name> -- /bin/sh


