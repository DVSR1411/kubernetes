Kubernetes Installation
Download kubectl:
  curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.19.6/2021-01-05/bin/linux/amd64/kubectl
  Add permissions: chmod +x ./kubectl
  Move to bin: mv ./kubectl /usr/local/bin
  Check version: kubectl version --client
Download eksctl:
  curl -sL "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar -xz -C /tmp
  Move to bin: mv /tmp/eksctl /usr/local/bin
  Check version: eksctl version
Configure to AWS: aws configure
To create a cluster use command:
eksctl create cluster --name mycluster1 --region ap-south-1 --node-type t2.small
To delete a cluster use command:
eksctl delete cluster --name mycluster1
