---
layout: post
title: commit message 변경
category: Git
---

`git commit -m "메세지"`를 실행했는데 메세지를 바꾸고 싶은 경우에 필요한 명령어입니다. `commit`이 `push`가 된 경우와 아닌 경우로 나누어 볼 수 있습니다.

## 1. 아직 `push`되지 않은 경우

1. `$ git commit --amend`

    - 텍스트 편집기로 들어가면 가장 상단에 메세지가 있는데, 그것을 수정하고 저장종료합니다.

2. `$ git push origin master`

## 2. `push`된 경우

1. git rebase -i HEAD~3

    1. 숫자3은 보여질 최근 commit message의 개수를 의미합니다.(6으로 변경시 최근 6개의 메세지가 출력됩니다.)

    2. 텍스트 편집기로 화면이 전환됩니다.

    3. 상단에 `pick`으로 시작되는 3개의 문단이 있습니다.

    4. 그것들 중에서 변경하고자 하는 메세지내용의 `pick` 부분을 `reword`로 변경합니다.

    5. 저장 종료

2. 이어서 뜨는 또 다른 텍스트 편집기 화면에서 변경하고자 하는 메세지를 입력한 후 저장 종료합니다.

3. `$ git push --force`
