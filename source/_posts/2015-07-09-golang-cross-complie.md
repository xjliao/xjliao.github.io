title: Golang 交叉编译
date: 2015-07-09 14:44:32
tags:
 - Golang
categories:
 - Golang
 
---

在此之前假设你的Golang环境已经设置好了  

mac 二进制包安装golang默认可以使用linux/windows/freebsd, GOARCH为amd64的交叉编译， 386需要手动添加

## 
##准备目标平台的包和工具文件
以下过程不是重新编译，安装go，而是添加对其他平台的支持。
###方式一

```bash
$ cd /usr/local/go/src
$ CGO_ENABLED=0 GOOS=linux GOARCH=386 ./make.bash
$ CGO_ENABLED=0 GOOS=windows GOARCH=386 ./make.bash
$ CGO_ENABLED=0 GOOS=freebsd GOARCH=386 ./make.bash
```

>CGO_ENABLED=0 表示交叉编译禁用cgo  
如果go文件夹是owner为root， 请使用sudo  

如果需要提高编译速度，加入。
```bash
./make.bash --no-clean
```

###方式二

```bash
brew install --cross-compile-all go 
```

安装完成后，我们可以看到 Go的安装目录下 多了这个平台特有的几个命令行工具。
  
各平台的GOOS和GOARCH参考 
<table>

</table>

OS                   ARCH                          OS version
linux                386 / amd64 / arm             >= Linux 2.6
darwin               386 / amd64                   OS X (Snow Leopard + Lion)
freebsd              386 / amd64                   >= FreeBSD 7
windows              386 / amd64                   >= Windows 2000


##编译成对应平台下的执行文件
到源代码目录下执行:

```bash
$ CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build
```

不带前面参数的 go build 只是编译出开发环境适用的执行文件。

## golang-crosscompile工具
下载地址  
[github.com/davecheney/golang-crosscompile]()  
使用方法  
[http://dave.cheney.net/2012/09/08/an-introduction-to-cross-compilation-with-go]()
###下载脚本
```bash
$ git clone git://github.com/davecheney/golang-crosscompile.git
$ source golang-crosscompile/crosscompile.bash
```

###编译支持所有平台
```bash
$ go-crosscompile-build-all
```
这个时间要花个几分钟

###查看平台的包
```bash
$ ls -1 $(go env GOROOT)/pkg
```

###使用交叉编译

```bash
$ go-linux-arm build
```

要不同平台的编译，替换即可, 如:go-windows-386 build 

为方面以后使用,将下面的加入到.bashrc或.zshrc

```bash
$ mkdir ~/.golang-crosscomplie
$ cp golang-crosscompile/crosscompile.bash  ~./golang-crosscomplie
$ source ~/.zshrc
```