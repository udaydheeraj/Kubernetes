k8s-lab/
 ├── Dockerfile
 ├── index.php
 └── deploy.yaml

# Build Image
docker build -t apache-podname:v1 .
# To verify image is built:
docker images
# Apply Deployment + Service
kubectl apply -f deploy.yaml svc.yaml

# Verify All Resources
Check deployment
kubectl get deploy

Check replica set
kubectl get rs

Check pods
kubectl get pods -o wide


Service load balancing

Deployment → RS → Pod lifecycle

Custom Docker image working

Service routing via kube-proxy
