---
layout: post
title: ssh로 라즈베리파이에 접속이 안 될 때
category: SingleBoard
---
노트북에서 ssh로 접속하려고 하는데 port22접속 거부가 나올 때가 있습니다.  

준비물: hdmi선, 모니터, usb키보드  
라즈베리파이 터미널로 들어가고 난 후  

```
pi@raspberrypi $ netstat -ntl
```
명령어를 쳐보면 22port가 안 떠있을 것입니다.
ssh 서비스를 시작하기 위해서

```
pi@raspberrypi:/etc/ssh $ sudo service ssh restart
pi@raspberrypi:/etc/ssh $ ssh localhost
```
를 차례대로 입력합니다.  
```
The authenticity of host 'localhost (::1)' can't be established.
ECDSA key fingerprint is 02:22:d2:bd:1c:61:e5:d8:e4:0e:52:0e:22:b4:92:31.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'localhost' (ECDSA) to the list of known hosts.
pi@localhost's password:

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Fri Nov 25 18:09:30 2016

SSH is enabled and the default password for the 'pi' user has not been changed.
This is a security risk - please login as the 'pi' user and type 'passwd' to set a new password.
```
위와 같은 결과화면이 나오면 정상입니다.  

그리고 나서 아래 명령어를 치면  
```
pi@raspberrypi:~ $ netstat -ntl
```
22번 포트가 열려있는 것을 확인할 수 있습니다.
```
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN
tcp6       0      0 :::22                   :::*                    LISTEN
```


하지만, 다시 **노트북**에서 ssh로 접속해도  
```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the RSA key sent by the remote host is
[...].
Please contact your system administrator.
Add correct host key in /home/sward/.ssh/known_hosts to get rid of this message.
Offending RSA key in /home/sward/.ssh/known_hosts:86
RSA host key for [...] has changed and you have requested strict checking.
Host key verification failed.
```
이런 메시지가 뜨면서 여전히 접속은 불가능한 상태입니다.  

노트북 터미널에서 아래 명령어를 입력합니다.  
```
$ ssh-keygen -R 라즈베리파이의_ip주소
```

이제 ssh접속이 가능해졌습니다.
```
$ ssh pi@172.30.1.5
```
