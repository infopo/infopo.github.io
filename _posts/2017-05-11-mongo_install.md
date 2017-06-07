---
layout: post
title: MongoDB 설치 (우분투, 싱글보드, 윈도우)
category: DB
---

## 우분투 

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

---

## 싱글보드

```
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt-get install mongodb-server

$ sudo service mongodb status

$ mongo
```

주의할 점: 싱글보드에 설치할 경우 용량은 2GB로 제한된다.
> NOTE: This is a 32 bit MongoDB binary.  
> 32 bit builds are limited to less than 2GB of data (or less with --journal).

---

## 윈도우

**windows에서 실행할 때에는 cmd를 총 2개 열어야 한다**

1. [msi 버전 다운로드](www.mongodb.com/download-center#community)
   - C:\Program Files\MongoDB\Server\3.4\bin (기본 설치 경로)
2. c:\에 mongodb\data\db 경로의 폴더를 만든다(db에 관한 내용들이 저장될 공간)

3. 아래 경로로 이동한 후  
   ```
   C:\Program Files\MongoDB\Server\3.4\bin> mongod --dbpath C:\mongodb\data\db
   ```
   
   - 입력하면 아래의 메세지가 출력이 된다.

   > 2017-04-03T10:28:37.234+0900 I NETWORK [thread1] waiting for connections on port 27017  

4. cmd를 하나 더 열고 `mongo`를 입력한다  
   ```
   C:\Program Files\MongoDB\Server\3.4\bin> mongo
   ```  
   
   - 메세지가 출력되고 mongo가 실행된다

   > MongoDB shell version v3.4.3  
   > connecting to: mongodb://127.0.0.1:27017  
   > MongoDB server version: 3.4.3  
   > Server has startup warnings:  
   > 2017-04-03T10:52:18.443+0900 I CONTROL [initandlisten]  
   > 2017-04-03T10:52:18.443+0900 I CONTROL [initandlisten] ** WARNING: Access contr ol is not enabled for the database.  
   > 2017-04-03T10:52:18.446+0900 I CONTROL [initandlisten] ** Read and wri te access to data and configuration is unrestricted.
   > 2017-04-03T10:52:18.447+0900 I CONTROL [initandlisten]  
   > 2017-04-03T10:52:18.449+0900 I CONTROL [initandlisten] Hotfix KB2731284 or late r update is not installed, will zero-out data files.  
   > 2017-04-03T10:52:18.453+0900 I CONTROL [initandlisten]  
   > \>  
