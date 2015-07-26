title: Linux ddos defense
date: 2013-07-26 14:44:32
tags:
 - Linux
categories:
 - Linux
 
---

[官网:http://deflate.medialayer.com/](http://deflate.medialayer.com/)
##About
(D)DoS Deflate is a lightweight bash shell script designed to assist in the process of blocking a denial of service attack. It utilizes the command below to create a list of IP addresses connected to the server, along with their total number of connections. It is one of the simplest and easiest to install solutions at the software level.

```bash
netstat -ntu | awk '{print $5}' | cut -d: -f1 | sort | uniq -c | sort -n
```

IP addresses with over a pre-configured number of connections are automatically blocked in the server's firewall, which can be direct iptables or Advanced Policy Firewall (APF). (We highly recommend that you use APF on your server in general, but deflate will work without it.)

##Notable Features

It is possible to whitelist IP addresses, via /usr/local/ddos/ignore.ip.list.
Simple configuration file: /usr/local/ddos/ddos.conf
IP addresses are automatically unblocked after a preconfigured time limit (default: 600 seconds)
The script can run at a chosen frequency via the configuration file (default: 1 minute)
You can receive email alerts when IP addresses are blocked.
##Installation
```bash
wget http://www.inetbase.com/scripts/ddos/install.sh
chmod 0700 install.sh
./install.sh
```
##Uninstallation
```bash
wget http://www.inetbase.com/scripts/ddos/uninstall.ddos
chmod 0700 uninstall.ddos
./uninstall.ddos
```
##Questions?

Although most things are explained on this page, if you have any further questions, you may contact the original developer of the script, Zaf.

##Ban ping
```bash
iptables -A INPUT -p icmp --icmp-type 8 -s 0/0 -j DROP
```
##Allow ping
```bash
iptables -D INPUT -p icmp --icmp-type 8 -s 0/0 -j DROP
```