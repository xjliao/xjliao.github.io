---
layout: post
title: "iptables: Setting chains to policy ACCEPT: security raw nat[FAILED]filter"
categories:
- Linux
tags:
- Linux 

--- 
Linode官方在iptables里加了一个security的规则链，但Centos不支持。    
于是就会有以下错误    

{% codeblock lang:bash %}
iptables: Setting chains to policy ACCEPT: security raw nat[FAILED]filter
{% endcodeblock %}

解决方案  
编辑/etc/init.d/iptables，找到：  
{% codeblock lang:shell %}
for i in $tables; do
        echo -n "$i "
        case "$i" in
            raw)
                $IPTABLES -t raw -P PREROUTING $policy \
                    && $IPTABLES -t raw -P OUTPUT $policy \
                    || let ret+=1
                ;;
{% endcodeblock %}

加入以下内容到“case "$i" in”下面：

{% codeblock lang:shell %}
security)
       $IPTABLES -t filter -P INPUT $policy \
           && $IPTABLES -t filter -P OUTPUT $policy \
           && $IPTABLES -t filter -P FORWARD $policy \
           || let ret+=1
       ;;
{% endcodeblock %}

如果是用得redhat centos之类得Linux操作系统,可能会影响到yum的使用, 需要修改

{% codeblock sh %}
[xjliao@li539-59 ~] sudo vim /usr/bin/yum
\#!/usr/bin/python2.6
{% endcodeblock %}

结果

{% codeblock lang:shell %}
for i in $tables; do
    echo -n "$i "
    case "$i" in
        security)
            $IPTABLES -t filter -P INPUT $policy \
                && $IPTABLES -t filter -P OUTPUT $policy \
                && $IPTABLES -t filter -P FORWARD $policy \
                || let ret+=1
            ;;
        raw)
            $IPTABLES -t raw -P PREROUTING $policy \
                && $IPTABLES -t raw -P OUTPUT $policy \
                || let ret+=1
            ;;
{% endcodeblock %}
