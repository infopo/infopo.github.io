---
layout: post
title: 오라클SQL(developers) 설치 (윈도우)
category: DB
---

- [Oracle 11g Windows 설치 1~4까지](http://www.allsoft.co.kr/bbs/board.php?bo_table=study4_2&page=){:target="_blank"}

- [Oracle Database 11g Release 2](http://www.oracle.com/technetwork/indexes/downloads/index.html#database){:target="_blank"}

---

# Setup 시작

※윈도우10에서 설치하면 .net framework 3.5 설치하라는 말이 나오는데, 프로그램 추가/삭제 항목에서 windows 기능 켜기/끄기로 들어가 .net framework 3.5를 클릭하고, 4.6은 해제한다.
3.5를 다 설치했으면 재부팅을 하고, 다시 같은 곳으로 들어가서 3.5를 해제하고 4.6만 클릭하여 설치를 진행한다.  
다시 재부팅하고 3.5, 4.6을 모두 켜놓는다.  
- [참고사이트1](http://click-me.tistory.com/169){:target="_blank"}  
- [참고사이트2](http://blog.naver.com/newzoen/220726156477){:target="_blank"}  

## 다운받은 폴더로 이동  
- 2/2 폴더 내의 파일들을 1/2폴더의 같은 위치에 복사한다  
- 1/2에 있는 setup파일을 실행  

1. 보안 갱신 구성
  1. 오라클 아이디/my oracle support 비밀번호 입력
  2. 접속 실패 팝업이 뜨면 ‘구성상의 중요 보안 문제에 대한 알림을 수신하지 않습니다.’ 클릭
2. 설치 옵션
  1. 데이터베이스 소프트웨어만 설치
3. Grid 설치 옵션
  1. 단일 인스턴스 데이터베이스 설치
4. 제품언어: 그대로 (선택된 언어 - 영어, 한국어)
5. 데이터베이스 버전
  1. Enterprise Edition
6. 설치 위치
  1. Oracle Base: C:\app\JW     (C드라이브로 되어 있는지 꼭 확인할 것)
  2. 소프트웨어 위치: C:\app\JW\product\11.2.0\dbhome_1
7. 요약: 그대로
8. 제품설치
  1. 중간에 방화벽 경고가 나오면 홈 네트워크 허용을 클릭하고 엑세스 허용을 클릭한다.
9.  완료

1521 포트가 기본으로 설정된 것(서버가 물리적으로 다른 곳에 있다면, 방화벽개방을 해줘야한다)  
오라클에서는 서버측의 리스너설치가 필요하고 클라이언트 측에서도 리스너접근을 위한 접속프로그램이 필요  

## 설치완료 후 다음경로로 이동  
C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Oracle - OraDb11g_home1\구성 및 이전 툴  
시작메뉴에서 새로 설치된 프로그램에도 있음  

---

## Database Configuration Assistant 실행  
(설치과정에서 sid입력하는 곳이 있었는지 확인해볼것) sid 입력넣는 곳있음. sid는 sql developer 접속에 필요하다  

1. 수행할 작업
  1. 데이터베이스 생성
2. 데이터베이스 템플리트
  1. 범용 또는 트랜잭션 처리
3. 데이터베이스 이름
  1. 전역 데이터베이스이름: acorn(임의로 정해도 됨)
  2. SID: acorn
4. 관리옵션
  1. enterprise manager 구성 해제
5. 데이터베이스 인증서
  1. 모든 계정에 동일한 관리 비밀번호 사용(오라클 비번과 동일하게 설정)
6. 데이터베이스 파일 위치
  1. oracle-manged-files 사용
7. 복구 구성: 변경사항 없음
8. 데이터베이스 내용
  1. 샘플 스키마 클릭
9. 초기화 매개변수
  1. 문자집합 탭 클릭 - 유니코드 사용
10. 데이터베이스 저장 영역: 변경사항 없음
11. 생성 옵션: 변경사항없음 → 완료
12. 데이터베이스 생성 - 요약 → 확인

## 설치진행  
중간에 ora-00922가 뜨는데 그냥 무시하면됨  
ora-28000도 뜨는데 또 무시하면 됨  

## 데이터베이스 생성완료팝업뜨면 비밀번호 관리 - SCOTT → 새비밀번호에 TIGER입력  
- [참고사이트1](http://www.allsoft.co.kr/bbs/board.php?bo_table=study4_2&wr_id=5){:target="_blank"}
- [참고사이트2](http://all4museum.tistory.com/entry/%EC%98%A4%EB%9D%BC%ED%81%B411g-DB-%EC%83%9D%EC%84%B1){:target="_blank"}

---

## 설치완료 후 다음경로로 이동  
C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Oracle - OraDb11g_home1\구성 및 이전 툴  

## net configuration assistant  
- 리스너 구성
  - 추가
  - 리스너명: acorn
  - 선택된 프로토콜: tcp
  - 표준포트번호 1521 사용
  - 방화벽: 홈 네트워크 허용
  - 다른 리스너구성? no
  - 완료  

- TCP
- 포트번호까지 다음다음
- 다른 리스너 구성 - 아니오 선택
- 다시 원래 화면으로 복귀함
- 추가
- 서비스이름: acorn (클라이언트 쪽)
- 완료

- 로컬 네트 서비스 이름 구성
  - 추가
  - 서비스이름:  acorn
  - 프로토콜: TCP
  - 호스트이름:  → 시스템속성 → 컴퓨터이름 → 전체 컴퓨터 이름 복붙 (USER-PC)  (컴터에 따라 다름)
    - 표준 포트번호 1521사용
  - 테스트 수행하시겠습니까? yes
  - 로그인변경: 아까 입력햇던 비번
  - 테스트 수행(대/소문자 확인할 것)
    - 실패 뜬다
    - 로그인변경 클릭 - 아까 입력한 비밀번호 입력
    - 테스트 성공! 뜸
  - 네트 서비스 이름: 입력 창이 나옴 → acorn
  - 다른네트 서비스 이름을 구성하겠습니까? → no
  - 네트 서비스 이름 구성이 완료되었습니다. → 다음 → 완료

---

## 설치완료 후 다음경로로 이동  
C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Oracle - OraDb11g_home1\응용 프로그램 개발  

- SQL Plus 실행
- sql plus(콘솔창)에서 &rarr; ALTER USER SCOTT ACCOUNT UNLOCK IDENTIFIED BY TIGER;  

---

## SQL Developer  
C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Oracle - OraDb11g_home1\응용 프로그램 개발  

- SQL Developer 실행  
- 실행이 안돼서 아래에서 추가 다운로드
[사이트](http://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/sqldev-downloads-415-3662249.html){:target="_blank"}  
- 경로: Oracle Technology Network - Developer Tools - SQL Developer - Downloads  
- ~~(4.2.0버전으로 다운 받을 것) jdk8포함버전을 받을 것~~  
- 4.1.5버전 다운 받을 것
    - SQL Developer 4.1.5
    - Version 4.1.5.21.78, Updated September 16, 2016
    - Windows 64-bit with JDK 8 included

- 다운받으로 파일을 C드라이브로 이동
- 다운받은 파일에서 exe파일을 실행
- 설치경로 설정에서 돋보기 누르면 자동으로 경로가 잡힘

---


# 삭제
- [참고사이트1](http://srzero.tistory.com/entry/ORACLE-11G-%EC%82%AD%EC%A0%9C-%EC%8A%A4%EC%83%B7snapshot){:target="_blank"}
- [참고사이트2](http://happytomorrow.net/86){:target="_blank"}

1. services.msc
  - oracle로 시작하는 서비스 중지
2. deinstaller
3. C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Oracle - OraDb11g_home1
  시작 메뉴 - 모든 프로그램 - Oracle - OraDb11g_home1 - Oracle 설치 제품 - Universal Installre
4. regedit
  - HKEY_LOCAL_MACHINE > SOFTWARE > ORACLE > 
5. 남은 폴더 지우기
  - C:\Users\USER\AppData\Roaming\SQL Developer         //숨겨진 폴더 보기해야 보임
  - C:\Program Files\Oracle
  - C:\app\USER\product\11.2.0\dbhome_1
  - C:\app\USER\oradata
