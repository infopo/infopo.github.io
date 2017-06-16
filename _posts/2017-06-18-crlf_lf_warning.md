---
layout: post
title: CRLF, LF warning 해결
category: Git
---

`$ git add .`를 했을 때 나타났던 오류 메세지입니다.

> warning: CRLF will be replaced by LF in 2017-05-10-acorn46_170106/0106jadetest/node_modules/void-elements/.gitattributes.  
The file will have its original line endings in your working directory.  

이것은 윈도우 계열과 유닉스 계열이 사용하는 줄바꿈문자의 차이 때문에 발생합니다. 유닉스 계열은 `line fedd(LF)`만 사용하지만, 윈도우 계열은 `line feed(LF)`와 `carriage return(CR)` 두가지를 모두 사용합니다(`CRLF`).

---

#### 해결

아래 명령어를 `git add`전에 입력하면 됩니다.
```
$ git config core.autocrlf true
```

예시
```
$ git config core.autocrlf true
$ git add .
$ git commit -m "add some files"
$ git push origin master
```
