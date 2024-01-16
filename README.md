# eks-increase-pod-count-per-node

1. Create a EKS cluster
2. Run those commands to update cluster cni config

```
kubectl set env daemonset aws-node -n kube-system ENABLE_PREFIX_DELEGATION=true
```
```
kubectl set env ds aws-node -n kube-system WARM_PREFIX_TARGET=2
```
3. Create a launch template.
Put this script in the "Advanced details->User data" section while creating a launch template.
Note: Please replace the "CLUSTER_NAME" field with your EKS cluster name.

```
MIME-Version: 1.0
Content-Type: multipart/mixed; boundary=569cf6b9fd8fc55eb154ed4109442d086eac9082ff292a37a3b3cd88bfb6
                                                                    
--569cf6b9fd8fc55eb154ed4109442d086eac9082ff292a37a3b3cd88bfb6
Content-Type: text/x-shellscript
Content-Type: charset="us-ascii"
                                                                    
#!/bin/sh
set -o xtrace
sudo /etc/eks/bootstrap.sh CLUSTER_NAME --use-max-pods false --kubelet-extra-args '--max-pods=110's
--569cf6b9fd8fc55eb154ed4109442d086eac9082ff292a37a3b3cd88bfb6--
```
4. Use that launch tempalte while creating a node group in the EKS cluster. 
Choose Add node group -> Configure node group -> Use launch template
