# Minikube single node Cluster : Pods 

Run these as ubuntu or a sudo user.

bash
# Update
sudo apt update && sudo apt upgrade -y

# Basic tools
sudo apt install -y curl wget apt-transport-https conntrack
Install Docker as Minikube’s driver:

bash
sudo apt install -y docker.io
sudo usermod -aG docker $USER
newgrp docker
Lab 1: Install kubectl and Minikube
Install kubectl:

bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
kubectl version --client
Install Minikube:

bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube version
Lab 2: Create single‑node Minikube cluster
Start the cluster using Docker driver:

bash
minikube start --driver=docker
Verify cluster and node:

# bash
kubectl cluster-info
kubectl get nodes -o wide
kubectl get pods -A
If STATUS of the node is Ready, your single‑node Kubernetes cluster is up.

Lab 3: Create a pod imperatively
Create an NGINX pod and expose it.

bash
# Simple pod
kubectl run nginx-pod --image=nginx --restart=Never

# Check pod
kubectl get pods
kubectl describe pod nginx-pod
Expose it via ClusterIP service:

# bash
kubectl expose pod nginx-pod --port=80 --name=nginx-service
kubectl get svc
You can test from inside the cluster:

# bash
kubectl run test-pod --rm -it --image=busybox --restart=Never -- wget -qO- nginx-service
Lab 4: Create pods using YAML
Create a YAML file:

# nginx-pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-yaml-pod
  labels:
    app: nginx
    env: dev
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80

Apply and inspect:

# bash
kubectl apply -f nginx-pod.yaml
kubectl get pods -l app=nginx
kubectl describe pod nginx-yaml-pod
kubectl get pods --show-labels
Delete resources when done:

# bash
kubectl delete pod nginx-pod nginx-yaml-pod
kubectl delete svc nginx-service
