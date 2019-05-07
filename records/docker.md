# docker的安装和使用
## centos7安装docker
### 1.查看内核版本
执行`uname -r`，内核版本要高于3.10才可以用这个方法安装，否则见[docker安装](http://www.runoob.com/docker/centos-docker-install.html)链接
### 2.开始安装
	yum -y install docker-io
### 3.启动 Docker 后台服务
`service docker start`或者`systemctl start docker`
### 4.问题处理：
#### 1)启动docker报错：

    Jul 04 10:19:38 cloud-blockchain10-dev systemd[1]: Starting Docker Application Container Engine...
    Jul 04 10:19:38 cloud-blockchain10-dev dockerd-current[549]: time="2018-07-04T10:19:38.282968952+08:00" level=warning msg="could not change...found"
    Jul 04 10:19:38 cloud-blockchain10-dev dockerd-current[549]: time="2018-07-04T10:19:38.285829512+08:00" level=info msg="libcontainerd: new ...: 557"
    Jul 04 10:19:39 cloud-blockchain10-dev dockerd-current[549]: Error starting daemon: SELinux is not supported with the overlay2 graph driver...false)
    Jul 04 10:19:39 cloud-blockchain10-dev systemd[1]: docker.service: main process exited, code=exited, status=1/FAILURE
    Jul 04 10:19:39 cloud-blockchain10-dev systemd[1]: Failed to start Docker Application Container Engine.
    Jul 04 10:19:39 cloud-blockchain10-dev systemd[1]: Unit docker.service entered failed state.
    Jul 04 10:19:39 cloud-blockchain10-dev systemd[1]: docker.service failed.
处理方式：

	vi /etc/sysconfig/docker

然后将--selinux-enabled 改成 --selinux-enabled=false，然后启动docker服务
#### 2)启动docker增加-H tcp://0.0.0.0:2375的访问方式
	vi /etc/sysconfig/docker
	OPTIONS="--selinux-enabled=false --log-driver=journald --signature-verification=false -H tcp://0.0.0.0:2375"

### 5.参考链接：
[docker安装](http://www.runoob.com/docker/centos-docker-install.html)
## ubuntu 安装docker
### 1.安装
	apt-get update
	apt install -y docker.io
### 2.启动docker后台服务
	service docker start
### 3.docker启动配置文件目录：
	/lib/systemd/system/docker.service
### 4.重启
	systemctl daemon-reload
	systemctl restart docker.service
## 安装docker-compose
### 1.下载
	curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
### 2.赋权
	chmod +x /usr/local/bin/docker-compose
### 3.测试安装结果
	docker-compose --version

## docker镜像导入导出
	docker save -o liuhy.tar hyperledger/fabric-zookeeper:0.4.10 hyperledger/fabric-kafka:0.4.10 hyperledger/fabric-couchdb:0.4.10 hyperledger/fabric-baseos:amd64-0.4.10
	scp liuhy.tar 目标机器
	docker load -i liuhy.tar
	删除tar包

## docker不用加sudo
### 1.创建一个docker组 
	sudo groupadd docker
### 2.添加当前用户到docker组 
	sudo usermod -aG docker $USER
### 3.登出，重新登录shell
### 4.验证docker命令是否可以运行
	docker ps 

## docker清理日志
	sudo find /var/lib/docker/containers/ -name *-json.log  -exec rm -f {} \;

## docker加速器配置
在docker的启动参数中加
```
--registry-mirror=https://7z4sr9d7.mirror.aliyuncs.com
```
[Docker - 配置国内加速器加速镜像下载](https://www.cnblogs.com/atuotuo/p/6264800.html)