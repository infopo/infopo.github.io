---
layout: post
title: Jupyter Lab 설치
category: Jupyter
---

Jupyter Notebook을 사용하다가 Jupyter Lab이 있다는 걸 알게 되었습니다. 현재도 Notebook 대신 Lab을 이용해 파이썬 코딩을 하는데요, 설치를 해보고 간단한 소개를 하도록 하겠습니다.  

Jupyter Notebook이 설치가 된 상태에서 진행을 해야 합니다. Jupyter Lab은 Jupyter Notebook의 설정들을 그대로 가져옵니다. 설치과정은 간단합니다.  

```
$ sudo pip install jupyterlab
$ sudo jupyter serverextension enable --py jupyterlab --sys-prefix
```

설치가 끝났습니다. 아래 명령어를 사용해 실행할 수 있습니다.

```
$ jupyter Lab
```

<br>

첫 화면입니다. Notebook과 다르게 좌측에 탭이 새로 생겼습니다. 홈 디렉토리를 Tree View로 볼 수도 있고, 명령어와 실행 중인 파일들을 볼 수도 있습니다. 탭을 한 번 더 클릭하면 최소화시킬 수도 있습니다. IDE와 같은 모습을 갖추게 된 것 같습니다.

[]({{ site.baseurl }}/images/jupyter_lab_1.png)

<br>

여러 개의 파일들을 실행한 화면입니다. Notebook에서는 웹브라우저의 새탭에 파일들을 띄워야 했는데, Lab에서는 웹브라우저 내의 한 화면에 파일들을 띄우고, 현재 위치도 좌측 Tree View에서 확인할 수 있어서 훨씬 편해졌습니다.  

[]({{ site.baseurl }}/images/jupyter_lab_2.png)

<br>

창 분할도 가능합니다.  

[]({{ site.baseurl }}/images/jupyter_lab_3.png)

<br>

내장된 터미널도 있습니다.  

[]({{ site.baseurl }}/images/jupyter_lab_4.png)

<br>

물론, 터미널에서 `jupyter notebook`을 따로 실행하지 않아도 Notebook을 실행할 수 있습니다. help 탭에서 Launch Classic Notebook을 클릭하면 됩니다.  

[]({{ site.baseurl }}/images/jupyter_lab_5.png)

---

참고할 사항  

- `Tab`버튼이 기존에는 코드 들여쓰기였는데, Lab에서는 `ctrl`+`[`와 `ctrl`+`]`로 변경되었습니다.

- 파일이 여러 개 열려있는 경우, `ctrl`+`shift`+`[`와 `ctrl`+`shift`+']'로 파일 간 이동이 가능합니다.

- 아직 preview단계라서 그런지 안 되는 기능들이 있는 것 같습니다. 예를 들어, markdown cell에서 `font color`가 인식되지 않습니다.
`### <font color='red'>abcd</p>`
