---
layout: post
title: wget 관련 - tar -vxzf 오류 발생할 때
category: Linux
---

wget으로 받은 java파일을 tar -vxzf하려고 할 때
```
gzip: stdin: not in gzip format
tar: Child returned status 1
tar: Error is not recoverable: exiting now
```
이런 오류가 발생하는 경우가 있습니다. 이건 다운로드 페이지에서 라이센스 동의를 할 때, 쿠키가 설정되기 때문입니다.

해결방법: __`--`no-cookies `--`header "Cookie: oraclelicense=accept-securebackup-cookie"__ 을 wget 뒤에 추가해주면 됩니다.
```
$ wget http://.tar.gz --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie"
```
