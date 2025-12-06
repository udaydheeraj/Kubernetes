# Kubernetes
Kubernetes:
*K8 designed : that containers will crash, machines will disappear, networks will fail, deployments will be interrupted, and traffic will fluctuate; k8 treats them as expected scenarios and builds automation around recovery, scaling, rescheduling, and reconciliation. 

Master(controller)- node architecture
* cluster: overlay networking : multiple hosts having container forming 
* Auto-scaling
* Auto-healing
* Enterprise level application support

Explain everything in detail topic and sub topics in-depth with examples : beginner friendly fresher language: tier 3 : real-time usecases : more than 10000 words(word count) : paragraph style (dont want bullet points) : give text based diagrams : give everything in 2 parts

K8s Architecture :
* Control plane[master] : core components - api server, scheduler, etcd , controller manager - [replicaset] , cloud controller manager(CCM) - [EKS, AKS]
* worker nodes : Pod :  kube-let, Container runtime, Kube-proxy[networking, IP, Load-balancing],   
* data plane
                                        
                                                                                                             
K8s Production Systems :
* Cluster : creation, upgrade, deletion 

* K8 distributions : kubernetes, openshift, Rancher, Tanzu, EKS, AKS, GKE, DKE

* devops engineer : manage 100’s of clusters : - KOPS[kubernetes operations], Kubeadm

* Lifecycle of kubernetes : managing clusters : use KOPS tool
* minikube

K8 : control plane(master) node : communicates through API server :
* components : etcd : persistant data store
* Schedular : watches for created pods and decide
* controller manager
* Cloud controller manager (CCD)


K8 Worker nodes : Kubelet, container runtime, Kube-proxy[networking]

install : Kubectl : commandline tool to talk to k8

Nodes, pods

local clusters: minikube, k3s, kind, microk8s for practise K8

minikube start —> VM : single node K8 cluster

installing pod : pod.yml file: kubectl apply -f pod.yml
kubectl get pods -o wide

minikube ssh [logging into cluster to connect to pod]
shell : curl 172.6.0.0


kubectl delete pod podname [to delete pod]
kubectl logs podname[to check the logs by pod name]
kubectl describe pod podname
kubectl get all -a


Pod vs node vs Deployment

Deployment : is k8 yaml manifest : provides us with auto-healing and auto-scaling
D creates a ReplicaSet : which is a K8 controller maintains the desired state same as Actual state
RS maintains the desired umber of pods mentioned in Deployment manifest running in the actual state node

Deployment —> Replica-set[RS](K8 controller) --> Pods

kubectl get pods -w
kubectl get deploy
kubectl get rs
kubesctl delete pod podname
