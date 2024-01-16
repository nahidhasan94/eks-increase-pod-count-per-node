# eks-increase-pod-count-per-node

1. Create a EKS cluster
2. Run those commands to update cluster cni config

```
kubectl set env daemonset aws-node -n kube-system ENABLE_PREFIX_DELEGATION=true
kubectl set env ds aws-node -n kube-system WARM_PREFIX_TARGET=2

```
