Goal of the Lab

Create a ConfigMap with environment variables

Use those variables inside an Apache container

Serve a web page that shows values from ConfigMap

Run everything on Minikube


Minikube (cluster)
 └── Pod (httpd)
      └── Container reads env vars from ConfigMap


minikube start
kubectl get nodes


kubectl apply -f configmap.yaml
kubectl describe configmap web-config


kubectl apply -f deployment.yaml
kubectl get pods


kubectl apply -f service.yaml
minikube ip
http://<minikube-ip>:30080


Verify env vars inside container
kubectl exec -it <pod-name> -- env | grep APP


You will see:

APP_NAME=ConfigMap Demo App
ENVIRONMENT=DEV
OWNER=Kubernetes Lab


ConfigMap
   ↓ (at pod creation)
Pod
   ↓
Container reads env vars
