# 命令

## 获取特定空间下的所有的pod
kubectl get pod -n 1xiangsu-dev

## 进入pod
kubectl exec -it museumserver-54758d4f9f-n47hz -n 1xiangsu-prod -- /bin/bash

# 集群重启所有pod
kubectl rollout restart deployment/test-k8s -n 1xiangsu-dev

## 删除deployment和所有的pod

kubectl delete deployment test-k8s -n 1xiangsu-dev