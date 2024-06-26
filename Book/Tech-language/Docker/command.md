# 命令

## 获取所有的pod
kubectl get pod -n 1xiangsu-dev

## 进入pod
kubectl exec socket-service-dev-6c9fb65594-6fh9r -it -n 1xiangsu-dev -- /bin

# 集群重启所有pod
kubectl rollout restart deployment/test-k8s -n 1xiangsu-dev