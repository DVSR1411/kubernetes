# ALB Ingress Controller Setup on EKS

## Step 1: Associate IAM OIDC Provider
Associate the IAM OIDC provider with your EKS cluster.
```sh
eksctl utils associate-iam-oidc-provider --cluster=test --approve
```
## Step 2: Apply RBAC Role
Apply the RBAC role required by the ALB Ingress controller.

```sh
kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/aws-alb-ingress-controller/v1.1.9/docs/examples/rbac-role.yaml
```
## Step 3: Create IAM Policy
Create an IAM policy for the ALB Ingress controller.
```sh
aws iam create-policy --policy-name ALBIngressControllerIAMPolicy --policy-document https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/main/docs/install/iam_policy.json
```
## Step 4: Create IAM Service Account
Create an IAM service account and attach the policy to it.
```sh
eksctl create iamserviceaccount \
  --cluster=test \
  --namespace=kube-system \
  --name=alb-ingress-controller \
  --attach-policy-arn=$PolicyArn \
  --override-existing-serviceaccounts \
  --approve
```
## Step 5: Add Helm Repository
Add the EKS Helm repository.
```sh
helm repo add eks https://aws.github.io/eks-charts
```
## Step 6: Apply CRDs
Apply the Custom Resource Definitions (CRDs) for the ALB Ingress controller.
```sh
kubectl apply -k "github.com/aws/eks-charts/stable/aws-load-balancer-controller/crds?ref=master"
```
## Step 7: Install ALB Ingress Controller
Install the ALB Ingress controller using Helm.
```sh
helm install aws-load-balancer-controller eks/aws-load-balancer-controller \
  -n kube-system \
  --set clusterName=test \
  --set region=ap-south-1 \
  --set vpcId=vpc-id \
  --set ingressClass=alb \
  --set serviceAccount.create=false \
  --set serviceAccount.name=alb-ingress-controller
```
## Step 8: Verification
After installation, verify that the AWS Load Balancer Controller is running:
```sh
kubectl get pods -n kube-system | grep aws-load-balancer-controller
```
This README file provides step-by-step instructions to set up the ALB Ingress controller on your EKS cluster. If you need further assistance or have any questions, feel free to ask! 😊
