---
layout: post
title: 'Hexo deploy rsync'
categories:
- Linux
tags:
- Linux

---

##First step: intall rsync on your server

{% codeblock lang:bash %}
yum install rsync -y
{% endcodeblock %}

##Second step: set the configuration file
Edit _config.yml
{% codeblock lang:bash %}
deploy:
- type: git
  repo: git@github.com:xjliao/xjliao.github.io.git
  branch: master
- type: rsync
  host: 0.0.0.0
  user: xjliao
  root: /home/xjliao/blogserver/html
  port: 22
  delete: true
  verbose: true
  ignore_errors: false
{% endcodeblock %}