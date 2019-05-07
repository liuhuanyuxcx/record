# 一、安装protoc
先下载你所在系统的可执行文件，然后解压，将解压后的bin/protoc拷贝到你的PATH下即可
- protoc源码地址：[https://github.com/protocolbuffers/protobuf]()
- protoc可执行文件下载地址:[https://github.com/protocolbuffers/protobuf/releases](),protoc-$VERSION-$PLATFORM.zip为你要下载的可执行文件包。

# 二、安装GoLang protoc 插件
    go get -u github.com/golang/protobuf/protoc-gen-go

# 三、安装gRPC runtime
    go get google.golang.org/grpc
由于墙的存在，只能手动从[https://github.com/grpc/grpc-go]()下载源码，然后在拷贝到上述目录。。

# 四、参考链接
- [gRPC 官方文档中文版 V1.0](http://doc.oschina.net/grpc?t=57966)