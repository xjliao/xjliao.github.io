title: Linux yum install last stable version for nginx
date: 2015-08-27 11:55:49
tags:
- Linux
- Nginx
categories:
- Linux
- Nginx

---
```bash
vim /etc/yum.repos.d/nginx.repo 
```

Centos
```sh
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
gpgcheck=0
enabled=1
```

RHEL
```sh
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/rhel/$releasever/$basearch/
gpgcheck=0
enabled=1
```

from:
[http://wiki.nginx.org/Install](http://wiki.nginx.org/Install)