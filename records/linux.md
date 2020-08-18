# 记录linux常用命令
### 查看linux系统CPU信息
- CPU总核数 = 物理CPU个数 * 每颗物理CPU的核数
- 总逻辑CPU数 = 物理CPU个数 * 每颗物理CPU的核数 * 超线程数
- 查看CPU信息（型号）： `cat /proc/cpuinfo | grep name | cut -f2 -d: | uniq -c`
- 查看物理CPU个数：`cat /proc/cpuinfo| grep "physical id"| sort| uniq| wc -l`
- 查看逻辑CPU的个数：`cat /proc/cpuinfo| grep "processor"| wc -l`
- 参考：[https://www.cnblogs.com/bugutian/p/6138880.html](https://www.cnblogs.com/bugutian/p/6138880.html)

### 查看内存槽数、哪个槽位插了内存，大小是多少
	dmidecode|grep -P -A5 "Memory Device" |grep Size

### linux系统目录结构说明
链接：[https://blog.csdn.net/mzl87/article/details/79673012]()

### 安装gcc和g++
	yum install gcc
	yum install -y gcc-c++

### 时间设置
#### 时区设置
    timedatectl set-timezone Asia/Shanghai
    timedatectl set-ntp true
链接：[https://www.cnblogs.com/zhi-leaf/p/6282301.html]()

#### 安装ntp
    yum install -y ntp

    service ntpd start  #开启ntp客户端服务
    service ntpd status
链接：[https://blog.csdn.net/u013712826/article/details/61938675/]()


### SSH无密码登录和ssh常用命令
链接：[https://blog.csdn.net/liu_qingbo/article/details/78383892]()


### 查看内网和外网IP
- 内网：`ifconfig -a`执行结果中`inet `后面跟的就是内网IP
- 外网：`curl ifconfig.me`

### 发邮件
配置好`/etc/mail.rc`后，执行下面的命令就可以发邮件，具体配置方法见链接：[https://blog.csdn.net/du1055669885/article/details/82561503]()

    echo "This is a test email." |mail -s "Test!" ssy-02411@163.com

### df -h无响应
可能是因为读取不到远程挂载点的信息，导致hang住了，如果只看本地文件系统的信息，可以改用`df -hl`来查看，就不会hang住了。
