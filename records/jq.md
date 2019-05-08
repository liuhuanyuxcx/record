# 一、安装jq
## 1.centos下安装jq
### 1）添加yum源
	wget http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
	rpm -ivh epel-release-latest-7.noarch.rpm
	yum repolist
### 2）安装
	yum install -y jq
## 2.ubuntu下安装jq
	apt-get -y update && apt-get -y install jq

# 二、使用jq
