First apply the metrics-server files
Next apply the HPA, HPA-server, HPA-install files
To increase the load use command
kubectl run -i --tty load-generator --rm --image=busybox:1.28 --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://hpa-demo-deployment; done"
We observe that no.of pods increase as load increases automatically. This concept is called Horizontal Pod Autoscaling