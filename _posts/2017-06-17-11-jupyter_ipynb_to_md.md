---
layout: post
title: .ipynb파일을 .md로 변경
category: Jupyter
---

`nbconvert`명령어를 사용합니다.

```
$ ipython nbconvert 파일이름.ipynb --to markdown
```

결과로 같은 디렉토리에 .md파일이 생기며, 만약 그림파일이 있었다면 파일이름_files라는 폴더가 생성되면서 해당 폴더에 .png파일들이 생성됩니다.

주의할 점: .ipynb파일이 한글 제목이면 안 됩니다. 영어로 변경 후 `nbconvert`명령어를 실행해야 합니다.
