## Edit kubernetes configmap
```sh
kubectl edit -n kube-system configmap/aws-auth
```
## In the file add mapUsers below mapRoles as
```sh
---
apiVersion: v1
data:
  mapRoles: >
    - groups:
      - system:bootstrappers
      - system:nodes
      rolearn: arn:aws:iam::user_name:role/eksctl-demo-nodegroup-ng-270a75ac-NodeInstanceRole-S9qejavfKfxG
      username: system:node:{{EC2PrivateDNSName}}
  mapUsers: |
    - userarn: arn:aws:iam::user_name:user/test
      username: test
      groups:
         - system:masters
```
