title: Install Supervisor on CentOS
date: 2015-12-06 22:30:23
tags:
- Linux
categories:
- Linux

---


CentOS default repository is very limited, and even if you install EPEL you will get old packages, in my case I needed to install Supervisor to manage my Django application, after trying to do it manually and through EPEL I ended up with the following setup.

##Install Needed Package

```bash
sudo yum install python-setuptools
sudo easy_install pip
sudo pip install supervisor
Setup Supervisor
```

We’ve already installed “Supervisor” globally, but we need to create its configuration, luckily it comes with default config:
```bash
echo_supervisord_conf > supervisord.conf
sudo cp supervisord.conf /etc/supervisord.conf
sudo mkdir /etc/supervisord.d/
sudo vim /etc/supervisord.conf


:
[include]
files = /etc/supervisord.d/*.conf
:
```

Next we need to set “Supervisor” to run automatically every time you restart your machine, we need to create /etc/rc.d/init.d/supervisord with the following content:

```bash
sudo vi /etc/rc.d/init.d/supervisord
#!/bin/sh
#
# /etc/rc.d/init.d/supervisord
#
# Supervisor is a client/server system that
# allows its users to monitor and control a
# number of processes on UNIX-like operating
# systems.
#
# chkconfig: - 64 36
# description: Supervisor Server
# processname: supervisord

# Source init functions
. /etc/rc.d/init.d/functions

prog="supervisord"

prefix="/usr/"
exec_prefix="${prefix}"
prog_bin="${exec_prefix}/bin/supervisord"
PIDFILE="/var/run/$prog.pid"

start()
{
       echo -n $"Starting $prog: "
       daemon $prog_bin --pidfile $PIDFILE
       [ -f $PIDFILE ] && success $"$prog startup" || failure $"$prog startup"
       echo
}

stop()
{
       echo -n $"Shutting down $prog: "
       [ -f $PIDFILE ] && killproc $prog || success $"$prog shutdown"
       echo
}

case "$1" in

 start)
   start
 ;;

 stop)
   stop
 ;;

 status)
       status $prog
 ;;

 restart)
   stop
   start
 ;;

 *)
   echo "Usage: $0 {start|stop|restart|status}"
 ;;

esac
```

Then make sure CentOS knows about it:

```bash
sudo chmod +x /etc/rc.d/init.d/supervisord
sudo chkconfig --add supervisord
sudo chkconfig supervisord on
sudo service supervisord start
```

##Sample Supervisor App

Here is a sample of Django App to be controlled and monitored by Supervisor, just put it:

```bash
sudo vi /etc/supervisord.conf

:
[program:shadowsocks-server]
command=/home/xjliao/goworkspace/bin/shadowsocks-server -c /etc/shadowsocks.json
autostart=true
autorestart=true

[program:nginx-blogserver]
command=/home/xjliao/blogserver/sbin/nginx
autostart=true
autorestart=true
:
```

from:  
<https://rayed.com/wordpress/?p=1496>