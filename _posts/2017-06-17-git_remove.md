---
layout: post
title: 파일 삭제
category: Git
---

## 파일 삭제

```
jw@jw-Lenovo ~/asdf $ ls
hoho.txt
```

1. rm명령어로 로컬에서 파일 삭제합니다.
    - `jw@jw-Lenovo ~/asdf $ git rm hoho.txt`
        > rm 'hoho.txt'

2. 변경 내용을 확정합니다.
    - `jw@jw-Lenovo ~/asdf $ git commit -m "remove hohohohohoh"``
        > [master 1ce3aa7] remove hohohohohoh  
 1 file changed, 0 insertions(+), 0 deletions(-)  
 delete mode 100644 hoho.txt  

3. 파일 삭제를 실행합니다.
    - `jw@jw-Lenovo ~/asdf $ git push origin master`
        > Username for 'https://github.com': jongwoo315  
Password for 'https://jongwoo315@github.com':  
Counting objects: 2, done.  
Writing objects: 100% (2/2), 191 bytes | 0 bytes/s, done.  
Total 2 (delta 0), reused 0 (delta 0)  
To https://github.com/jongwoo315/asdf.git  
  1c0be84..1ce3aa7 master -> master  

## 파일 삭제 취소

```
$ git rm asdfasdf.txt
```

folder 통채로 삭제하려면 -r 추가하면 됩니다.
```
$ git rm -r work_directory
```

```
$ git reset
$ git checkout -- work_directory
```
