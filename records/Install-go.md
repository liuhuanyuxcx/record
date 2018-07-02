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