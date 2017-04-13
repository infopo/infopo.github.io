---
layout: post
title: raspberry 파이에 설치된 mysql에 원격 접속하기
category: SingleBoard
---

노트북 및 데스크탑에서 싱글보드컴퓨터(라즈베리파이 등)의 mysql에 접속하는 방법을 알아보겠습니다.  

우선 **라즈베리파이**에 접속합니다.  
127.0.0.1:3306으로 뜨면 로컬에서만 접속이 가능하다는 뜻입니다.  
```
$ netstat -ntl

Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
tcp        0      0 127.0.1.1:53            0.0.0.0:*               LISTEN     
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN
```
<br>
<br>
아래 경로로 들어갑니다.  
```
$ sudo vi /etc/mysql/my.cnf  # 여기에 bind-address 항목이 없다면 아래 경로로 시도
$ sudo vi /etc/mysql/mysql.cnf
```


아래처럼 변경을 하고 저장, 종료합니다.  
```
#bind-address=127.0.0.1  # 원래 127.0.0.1로 설정된 것은 주석처리
!includedir /etc/mysql/conf.d/
!includedir /etc/mysql/mysql.conf.d/

# 아래 명령어 추가
[mysqld]
bind-address    = 0.0.0.0
```


mysql을 다시 시작합니다.
```
$ service mysql restart

==== AUTHENTICATING FOR org.freedesktop.systemd1.manage-units ===
Authentication is required to restart 'mysql.service'.
Authenticating as: jwpi,,, (jwpi)
Password: 
==== AUTHENTICATION COMPLETE ===
```


127.0.0.1:3306이 0.0.0.0:3306으로 변경된 것을 확인할 수 있습니다.  
```
$netstat -ntl

Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
tcp        0      0 0.0.0.0:3306            0.0.0.0:*               LISTEN     
```


mysql에 접속하여 아래 명령어를 차례대로 입력합니다.  
```
$mysql -u root -p

mysql> use mysql;
mysql> grant all privileges on *.* to 'root'@'%' identified by 'root의 패스워드';
Query OK, 0 rows affected (0.03 sec)

# mariadb에서는 password 필드가 있기 때문에 password로 써도 되지만, 
# mysql에서는 password 필드가 authentication_string로 변경이 되었습니다.
mysql> select host, user, authentication_string from user;
+----------------------+------------------+-------------------------------------------+
| host                 | user             | authentication_string                     |
+----------------------+------------------+-------------------------------------------+
| localhost            | root             | *23AE809DDACAF96AF0FD78ED04B6A265E05AA257 |
| localhost            | mysql.sys        | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE |
| localhost            | debian-sys-maint | *1E0873EF2541AA095FD0BCE1FA0F49C91BE86F31 |
| %                    | root             | *23AE809DDACAF96AF0FD78ED04B6A265E05AA257 |
+----------------------+------------------+-------------------------------------------+
root 계정의 host 필드에 % 가 등록되었는지 확인한다. (% 표시된 host가 생겼으면 성공)

mysql> flush privileges;
Query OK, 0 rows affected (0.00 sec)

mysql> exit
```

다시 한 번 mysql을 재시작합니다.  
```
$ service mysql restart
```


이제, 노트북이나 데스크탑에서 라즈베리파이의 mysql에 접속해봅시다.(외부에서 접속할 경우에는 포트포워딩이 필요함)  
```
노트북사용자@노트북호스트 $ mysql -u root -h 라즈베리파이ip주소 -p
```
