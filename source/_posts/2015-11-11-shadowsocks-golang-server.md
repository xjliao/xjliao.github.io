title: Deploy shadowsocks-goalang server
date: 2015-08-27 11:55:49
tags:
- Linux
- shadowsocks
categories:
- Linux
- shadowsocks

---

## Get golang and set golang path  
```bash
wget https://storage.googleapis.com/golang/go1.5.1.linux-amd64.tar.gz
tar -zxvf /home/xjliao/go1.5.1.linux-amd64.tar.gz
mkdir /home/xjliao/goworkspace
sudo vim /etc/profile
go
```
Use go cmd to test.  

add
```bash
GOROOT=$HOME/go
GOPATH=$HOME/goworkspace

PATH=$PATH:$GOROOT/bin

export GOROOT GOPATH PATH
```



## Get shadowsocks-goalang  

```bash
go get github.com/shadowsocks/shadowsocks-go/cmd/shadowsocks-server
```

And then. We can look for a execute file at $GOPATH/bin name's shadowsocks-server.   
Ok. We need a configuration file to run the shadowsocks-server command.  
So....   

```bash
sudo vim /etc/shadowsocks.json
```

add
```bash
{
    "server":"0.0.0.0",
    "local_address": "127.0.0.1",
    "local_port":1080,
    "port_password":{
        "8383":"1"
    },
    "timeout":600,
    "method":"aes-128-cfb",
    "fast_open": false
}
```
Execute shadowsocks-server command. if do right steps, it will run at listener your set port and work well.
```bash
/home/xjliao/goworkspace/bin/shadowsocks-server/ -c /etc/shadowsocks.json
```

## Make it autostart when system start or reboot.  
Install supervisor and edit configuration file.

```bash
sudo yum install supervisor
sudo vim /etc/supervisord.conf
sudo chkconfig supervisord on
```
Add
```bash
[program:shadowsocks-server]
command=/home/xjliao/goworkspace/bin/shadowsocks-server -c /etc/shadowsocks.json
autostart=true              ; start at supervisord start (default: true)
autorestart=true            ; retstart at unexpected quit (default: true)
```


