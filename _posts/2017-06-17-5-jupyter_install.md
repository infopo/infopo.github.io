---
layout: post
title: Jupyter Notebook 설치
category: Juypter
---

## 설치

설치에 앞서 `update`부터 합니다.
```
$ sudo apt-get update
```

<br>

```
$ sudo apt-get -y install python-pip python-dev
```
우분투에는 파이썬이 기본으로 설치가 되어있지만, 혹시 파이썬이 없다면 `python2.7`도 `apt-get`으로 설치해줍니다.

<br>

`python`과 `pip`버전을 확인해봅니다.
```
$ python --version
$ pip --version
```

<br>

`pip`와 `jupyter`를 설치합니다.
```
$ sudo -H pip install --upgrade pip
$ sudo -H pip install jupyter
```

<br>

설치가 완료되었습니다. 이제 아래 명령어로 `jupyter notebook`을 실행합니다.
```
$ jupyter notebook
```

---

## 설정 파일 생성

`jupyter notebook`에 관한 다양한 설정을 할 수 있는 파일을 생성해보겠습니다. ip주소, 포트번호, 사용할 브라우저 등등을 설정할 수 있는데요, 여기서는 `jupyter`의 홈 디렉토리를 설정해보겠습니다.

`jupyter notebook --generate-config`를 터미널에서 실행하면 `/home/사용자명/.jupyter`디렉토리가 생성되고, `jupyter_notebook_config.py`라는 파일이 생성됩니다. 이 파일로 들어가 `#c.NotebookApp.notebook_dir = u''`로 이동한 다음, 주석을 지우고 적당한 위치를 디렉토리로 설정하면 됩니다.

예시
```
c.NotebookApp.notebook_dir = u'/home/jw/Documents/[PYTHON]/'
```
