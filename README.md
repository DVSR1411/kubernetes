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
