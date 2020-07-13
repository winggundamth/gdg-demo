# GDG Demo

## Prequisite

* gcloud with initial account and project
* kubectl
* helm

## Kubernetes Tutorials

### Create GKE Cluster

```bash
gcloud container clusters create gdg-demo --num-nodes 4 --zone asia-southeast1-a
# Wait for few minutes
```

* Walkthrough GKE features
  * Create Cluster with one click
  * High Availability Cluster
  * Choose Kubernetes Version
  * Create pools and choose number of nodes
  * Nodes autoscaling
  * Size of nodes
  * Preemptible nodes
  * Networking to do private cluster
  * Shielded GKE Nodes
  * Create GKE Cluster with command line
  * See created cluster for one click upgrade available option

### Deploy Pod

```bash
kubectl apply -f 01-pod.yaml
kubectl get pod
kubectl exec -it linux -c busybox -- sh
ping www.google.com
kubectl exec -it linux -c alpine -- sh
ping www.google.com
```

* Walkthrought Workloads Dashboard
  * Overview configuration
  * CPU, Memory, Disk
  * Events
  * Logs
  * YAML

### Deploy Nginx Deployment

```bash
kubectl apply -f 02-deployment.yaml
kubectl get deployment
kubectl get pod
watch kubectl get pod
# Scale replica to 3 on dashboard
```

### Deploy Nginx Service

```bash
kubectl apply -f 03-service-nginx-lb.yaml
kubectl get service -w
# Wait for few minutes until EXTERNAL-IP shows up
# Try to access to Nginx
```

* Walkthrough Services & Ingress Dashboard

### Deploy MariaDB with ClusterIP Service

```bash
kubectl apply -f 04-mariadb.yaml
kubectl get deployment
kubectl get pod -w
kubectl get service
# Wait for a minute to fully start MariaDB

# Test connect to MariaDB
kubectl exec -it linux -c busybox -- sh
telnet mariadb 3306
```

### Deploy Ingress

```bash
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm install ingress-nginx ingress-nginx/ingress-nginx
kubectl get deployment
kubectl get pod -w
kubectl get service -w
# Try to access to http://ipaddress
```

* Deploy Ingress to Nginx Service

```bash
kubectl apply -f 05-ingress-to-nginx.yaml
# Try to access from http://ipadress/nginx
```

* Deploy Ingress to Apache Service

```bash
kubectl apply -f 06-apache.yaml
# Try to access from http://ipadress/apache
```

### Namespace

```bash
kubectl get namespace
kubectl create namespace dev
kubectl get namespace
kubectl apply -f 02-deployment.yaml --namespace dev
kubectl get pod
kubectl get pod --namespace dev
```

### Rolling Update

```bash
watch -n1 kubectl get pod
# Rolling Update on Dashboard to httpd image
```

### Bonus install Wordpress with Helm

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
helm install wordpress bitnami/wordpress
kubectl get pod -w
kubectl get service -w
# Access via http://ipaddress
```

### Destroy Everything

```bash
gcloud container clusters delete gdg-demo --zone asia-southeast1-a
```
