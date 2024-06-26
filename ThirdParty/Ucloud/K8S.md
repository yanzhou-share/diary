# 创建集群token
kubectl -n kubernetes-dashboard create token kubernetes-dashboard --duration=1h

# 集群重启所有pod

kubectl rollout restart deployment/test-k8s -n 1xiangsu-dev