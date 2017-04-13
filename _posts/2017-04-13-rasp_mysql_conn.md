---
layout: post
title: raspberry 파이에 설치된 mysql에 원격 접속하기
category: SingleBoard
---

노트북 및 데스크탑에서 싱글보드컴퓨터(라즈베리파이 등)의 mysql에 접속하는 방법을 알아보겠습니다.  

우선 라즈베리파이에 접속합니다.  

```
$ netstat -ntl

Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
tcp        0      0 127.0.1.1:53            0.0.0.0:*               LISTEN     
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN
```
위 처럼 127.0.0.1:3306으로 뜨면 로컬에서만 접속이 가능하다는 뜻입니다.  
