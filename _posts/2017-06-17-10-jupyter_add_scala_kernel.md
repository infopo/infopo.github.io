---
layout: post
title: Scala kernel 추가
category: Jupyter
---

`Scala`설치가 선행되어야 합니다.  

<br>

`~/.bashrc`에 다음을 추가합니다.
```vim
export HOME=/home/jw
export PATH=$PATH:$HOME/bin
```
`source`로 변경사항을 적용합니다.

<br>

홈디렉토리 `/home/jw`에 `bin`이라는 디렉토리를 만듭니다. 그리고 나서 아래 명령어를 입력합니다.
```
$ curl -L -o coursier https://git.io/vgvpD && chmod +x coursier
$ mv coursier bin
```

<br>

이어서 `jupyter-scala.git`을 다운받고 설치를 계속합니다.
```
$ git clone https://github.com/alexarchambault/jupyter-scala.git
$ cd jupyter-scala
```

<br>

`jupyter-scala`파일에 들어가 현재 스칼라 버전에 맞게 파일을 수정을 해야 합니다.
```vim
#SCALA_VERSION=2.11.8
SCALA_VERSION=2.12.1
```

<br>

`jupyter-scala`를 실행합니다.
```
jupyter-scala $ ./jupyter-scala
```

<br>

이제 kernel 리스트에 scala가 추가된 것을 확인할 수 있습니다.
```
$ jupyter kernelspec list
```
> scala /home/jw/.local/share/jupyter/kernels/scala
