## Kubernetes Installation

### Download kubectl:
```sh
curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.33.0/2025-05-01/bin/linux/amd64/kubectl
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
