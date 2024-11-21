## Kubernetes Installation

### Download kubectl:
```sh
curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.19.6/2021-01-05/bin/linux/amd64/kubectl
```
**Add permissions:**
```sh
chmod +x ./kubectl
```
**Move to bin:**
```sh
mv ./kubectl /usr/local/bin
```
**Check version:**
```sh
kubectl version --client
```

### Download eksctl:
```sh
curl -sL "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar -xz -C /tmp
```
**Move to bin:**
```sh
mv /tmp/eksctl /usr/local/bin
```
**Check version:**
```sh
eksctl version
```
**Configure to AWS:**
```sh
aws configure
```

### To create a cluster use command:
```sh
eksctl create cluster --name mycluster1 --region ap-south-1 --node-type t2.small
```

### Update kubernetes config file:
```sh
aws eks update-kubeconfig --name mycluster1 --region ap-south-1
```

### To delete a cluster use command:
```sh
eksctl delete cluster --name mycluster1
```

## Monitoring Kubernetes cluster with helm

### Create a namespace eg: prometheus:
```sh
kubectl create namespace prometheus
```

### Download helm:
```sh
choco install kubernetes-helm -y
sudo dnf install helm -y
```

### Install helm packages:
```sh
helm repo add stable https://charts.helm.sh/stable
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm search repo prometheus-community
helm install stable prometheus-community/kube-prometheus-stack -n prometheus
```

### Change service type LoadBalancer for prometheus and grafana:
```sh
kubectl edit svc stable-kube-prometheus-sta-prometheus -n prometheus
kubectl edit svc stable-grafana -n prometheus
```

### Login to prometheus and grafana:
Open the prometheus using loadbalancer ipaddr:9090

Open the grafana using loadbalancer ipaddr username: admin, password: prom-operator
