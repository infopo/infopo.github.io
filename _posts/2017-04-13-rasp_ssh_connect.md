---
layout: post
title: ssh로 라즈베리파이에 접속이 안 될 때
category: SingleBoard
---
노트북에서 ssh로 접속하려고 하는데 port22접속 거부가 나올 때

라즈베리파이에 hdmi와 usb키보드를 연결하고(hdmi 인식을 잘 못하는 경우가 있다...)
라즈베리파이 터미널로 들어가고 난 후

pi@raspberrypi $ netstat -ntl
하면 22port가 안 떠있을 것이다

pi@raspberrypi:/etc/ssh $ sudo service ssh restart

pi@raspberrypi:/etc/ssh $ ssh localhost
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

pi@raspberrypi:~ $ netstat -ntl
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN
tcp6       0      0 :::22                   :::*                    LISTEN

그리고 나서 노트북에서 ssh로 접속하면
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

이런 메시지가 뜨는데,
노트북에서

$ ssh-keygen -R *ip_address_or_hostname*
$ ssh-keygen -R 172.30.1.5

$ ssh pi@172.30.1.5

이렇게 하면 된다.
