# 遇到的问题

1、80默认向443跳转，导致ipaynow回调业务服务器报308问题

解决方案：

k8s中的ingress 添加禁止跳转

ammotations:
    nginx.ingress.kubernetes.io/force-ssl-redirect: "false"
    nginx.ingress.kubernetes.io/ssl-redirect: "false"