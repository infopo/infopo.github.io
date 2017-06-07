---
layout: post
title: Node.js 설치
category: etc
---

[참고사이트](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-an-ubuntu-14-04-server){:target="_blank"}  

```
$ sudo apt-get update
$ sudo apt-get upgrade

$ curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
$ sudo apt-get install -y nodejs
```

버전 확인  
```
$node -v
```
