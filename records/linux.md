# 记录linux常用命令
### 查看linux系统CPU信息
- CPU总核数 = 物理CPU个数 * 每颗物理CPU的核数
- 总逻辑CPU数 = 物理CPU个数 * 每颗物理CPU的核数 * 超线程数
- 查看CPU信息（型号）： `cat /proc/cpuinfo | grep name | cut -f2 -d: | uniq -c`
- 查看物理CPU个数：`cat /proc/cpuinfo| grep "physical id"| sort| uniq| wc -l`
- 查看逻辑CPU的个数：`cat /proc/cpuinfo| grep "processor"| wc -l`
- 参考：[https://www.cnblogs.com/bugutian/p/6138880.html]()

### 查看内存槽数、哪个槽位插了内存，大小是多少
	dmidecode|grep -P -A5 "Memory Device" |grep Size

### linux系统目录结构说明
链接：[https://blog.csdn.net/mzl87/article/details/79673012]()

### 安装gcc和g++
	yum install gcc
	yum install -y gcc-c++ 