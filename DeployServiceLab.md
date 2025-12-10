Deployment + Service (production approach)
Step 1: Create Deployment YAML

Create file http-deploy.yaml:

apiVersion: apps/v1
kind: Deployment
metadata:
  name: http-deploy
spec:
  replicas: 3
  selector:
    matchLabels:
      app: http-deploy
  template:
    metadata:
      labels:
        app: http-deploy
    spec:
      containers:
      - name: http
        image: nginxdemos/hello
        ports:
        - containerPort: 80


Apply:

kubectl apply -f http-deploy.yaml


Check:

kubectl get deploy
kubectl get rs
kubectl get pods


✅ You will see:

1 Deployment

1 ReplicaSet (created by Deployment)

3 Pods

Step 2: Expose Deployment
kubectl expose deployment http-deploy \
  --type=NodePort \
  --port=80 \
  --name=http-deploy-svc


Access:

minikube service http-deploy-svc

Step 3: Rolling update (real production behavior)

Update image version:

kubectl set image deployment/http-deploy http=nginxdemos/hello:latest


Watch rollout:

kubectl rollout status deployment http-deploy


Check ReplicaSets:

kubectl get rs


✅ You’ll see:

Old ReplicaSet scaling down

New ReplicaSet scaling up

Zero downtime

Step 4: Rollback (power of Deployment)
kubectl rollout undo deployment http-deploy


✅ App instantly returns to previous version.

Final comparison (labs summary)

Text diagram:

LAB 1:
Pod → Service → Public
(no self-healing)

LAB 2:
Deployment → ReplicaSet → Pods → Service → Public
(self-healing + load balancing + rollouts)

Core takeaway (remember this forever)

Pod is temporary
ReplicaSet maintains count
Deployment manages life cycle
Service exposes network access
