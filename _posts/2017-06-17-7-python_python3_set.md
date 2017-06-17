---
layout: post
title: Python3 패키지 설치환경 설정
category: Python
---

우분투는 기본적으로 Python3가 설치된 상태입니다. 이제 패키지 관리가 가능하도록 몇 가지를 설치하도록 하겠습니다. 그러기 위해서는 `pip`가 필요합니다.  

```
$ sudo apt-get install python3-pip
$ sudo pip3 install --upgrade pip
$ sudo apt-get install python3-setuptools
```

<br>

`pip3 -V`혹은 `pip3 --version`를 통해 `pip`가 제대로 설치되었는지 확인하면 됩니다.  

패키지를 하나 설치해보겠습니다.  
```
$ sudo pip3 install numpy
```

<br>

설치된 패키지 확인은 `pip3 freeze | grep numpy`로 가능합니다. 설치된 모든 패키지를 확인할 때에는 `pip3 freeze`를 입력하면 됩니다.
