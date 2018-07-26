# centos7 安装使用nfs
## 一、服务端安装
### 1.安装 NFS 服务器所需的软件包：
	yum install -y nfs-utils
### 2.编辑exports文件，添客户端机器
    vim /etc/exports：
    /home/nfs/ 192.168.248.0/24(rw,sync,fsid=0)
同192.168.248.0/24一个网络号的主机可以挂载NFS服务器上的/home/nfs/目录到自己的文件系统中，rw表示可读写；sync表示同步写，fsid=0表示将/data整个目录包装成根目录
### 3.启动nfs服务
- 先为rpcbind和nfs做开机启动：(必须先启动rpcbind服务)

		systemctl enable rpcbind.service
		systemctl enable nfs-server.service
- 然后分别启动rpcbind和nfs服务：

		systemctl start rpcbind.service
		systemctl start nfs-server.service
- 确认NFS服务器启动成功：

		rpcinfo -p
- 检查 NFS 服务器是否挂载我们想共享的目录 /home/nfs/：

		exportfs -r
- 使配置生效

		exportfs 
## 二、客户端安装
### 1.安装 NFS 服务器所需的软件包：
	yum install -y nfs-utils
### 2.启动nfs服务
- 先为rpcbind做开机启动：

		systemctl enable rpcbind.service
- 然后启动rpcbind服务：

		systemctl start rpcbind.service
- 检查 NFS 服务器端是否有目录共享：

		showmount -e nfs服务器的IP
- 在从机上使用 mount 挂载服务器端的目录/home/nfs到客户端某个目录下：
		
		cd /home && mkdir /nfs
		mount -t nfs 192.168.248.208:/home/nfs /home/nfs
- 查看是否挂载成功：

		df -h  #或者：
		mount | grep nfs
### 参考链接：[https://www.cnblogs.com/lixiuran/p/7117000.html]()