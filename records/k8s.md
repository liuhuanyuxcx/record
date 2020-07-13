# k8s常用命令举例
### 1.强制删除pod
`kubectl delete pod [pod name] --force --grace-period=0 -n [namespace]`
