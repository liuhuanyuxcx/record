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
## 安装docker-compose
### 1.下载
	curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
### 2.赋权
	chmod +x /usr/local/bin/docker-compose
### 3.测试安装结果
	docker-compose --version

