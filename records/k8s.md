# k8s常用命令举例
### 1.强制删除pod
`kubectl delete pod [pod name] --force --grace-period=0 -n [namespace]`

### 2.k8sdns出问题排查经验
`sysctl net.ipv4.ip_forward`查看结果，如果`net.ipv4.ip_forward = 0`，则需要改成1后重启docker。
#### 修改方式1-临时修改
  sysctl -w net.ipv4.ip_forward=1
#### 修改方式2-永久修改
```  
  cat <<EOF >  /etc/sysctl.d/k8s.conf
  net.bridge.bridge-nf-call-ip6tables = 1
  net.bridge.bridge-nf-call-iptables = 1

  vm.swappiness = 0
  net.ipv4.ip_forward = 1

  net.ipv4.tcp_timestamps = 1
  net.ipv4.tcp_tw_recycle = 1 

  net.ipv4.tcp_fin_timeout = 30
  net.ipv4.tcp_tw_resue = 1
  EOF

  sysctl --system
```
注意：/etc/sysctl.conf,/etc/sysctl.d/k8s.conf,/etc/sysctl.d/kubernetes.conf这三个文件都要看
