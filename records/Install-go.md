# Go语言环境安装
## 1.下载go安装包
- [官网地址](https://golang.org/dl)
- [墙内地址](https://studygolang.com/dl)

## 2.安装
点击安装包傻瓜安装，或者解压到指定目录

## 3.配置环境变量
- GOROOT：go安装的位置，如果是安装包安装，会自动配置；如果是解压，需要自己讲解压目录配置成GOROOT
- GOPATH：go工程文件放置的位置，需要自行配置
	- GOPATH目录结构：
		- src：源代码
		- pkg：编译后的包文件
		- bin：编译后的可执行文件

### 3.go get被墙的解决方法
[https://blog.csdn.net/ys5773477/article/details/73929161]() 


go get -u google.golang.org/grpc

由于墙的原因，我们一些依赖的包文件可以通过下面方式下载到：
在 github 可以找到源码，下载后复制到对应目录即可的：

- google.golang.org/grpc 对应的代码地址在： https://github.com/grpc/grpc-go
- google.golang.org/cloud/compute/metadata 对应的代码地址在： https://github.com/GoogleCloudPlatform/gcloud-golang
- golang.org/x/oauth2 对应的代码地址在： https://github.com/golang/oauth2
- golang.org/x/net/context 对应的代码地址在： https://github.com/golang/net 

### 4.go包管理演进史
[Go包管理的演进历史](https://tonybai.com/2017/06/08/first-glimpse-of-dep/)