## Monitoring Kubernetes cluster with helm

### Create a namespace eg: prometheus:
```sh
kubectl create namespace prometheus
```

### Download helm:
```sh
choco install kubernetes-helm -y #For Windows
```
```sh
sudo dnf install helm -y #For linux
```

### Install helm packages:
```sh
helm repo add stable https://charts.helm.sh/stable
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm search repo prometheus-community  #To find kube-prometheus-stack
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
