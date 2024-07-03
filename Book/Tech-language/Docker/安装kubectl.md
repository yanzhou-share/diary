# windows安装步骤

http://www.hzhcontrols.com/new-1959254.html

1、winget install -e --id Kubernetes.kubectl

2、kubectl version --client

3、将kubeConfig 写到本地文件  默认路径C:\Users\Administrator\.kube\config

4、kubectl cluster-info

如果加载自定义的config文件 

kubectl --kubeconfig /path/to/your/custom-kubeconfig get pods