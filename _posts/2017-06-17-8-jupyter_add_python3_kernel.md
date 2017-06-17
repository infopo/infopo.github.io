---
layout: post
title: Python3 kernel 추가
category: Jupyter
---

Python3 패키지 관리를 가능하게 해주는 `pip3`가 설치되어 있어야 합니다. 터미널에 아래 명령어를 입력합니다.  
```
$ sudo pip3 install jupyter
$ sudo ipython3 kernelspec install-self
```

<br>

이제 `jupyter notebook`이나 `jupyter lab`을 실행하고 새 노트북 추가를 누르면 kernel 목록에서 Python3를 확인할 수 있습니다.
