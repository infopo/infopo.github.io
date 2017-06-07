---
layout: post
title: MongoDB 설치
category: DB
---

우분투 16.04LTS 기준  

[참고사이트1](https://www.digitalocean.com/community/tutorials/how-to-install-mongodb-on-ubuntu-16-04){:target="_blank"}  

[참고사이트2](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/){:target="_blank"}  
삭제 방법도 있음  

```
$ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6   #공식
$ echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list

$ sudo apt-get update
$ sudo apt-get upgrade

$ sudo apt-get install -y mongodb-org

$ sudo service mongodb start
$ sudo service mongodb status
```
