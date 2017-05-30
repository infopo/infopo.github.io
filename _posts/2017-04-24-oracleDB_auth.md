---
layout: post
title: 오라클SQL 권한 부여
category: DB
---


## 기본적인 권한 부여

ID가 user1, Password는 tiger로 계정을 생성하겠습니다.  
```
SQL> CONN system/비밀번호
SQL> SHOW USER;

SQL> CREATE USER user1 IDENTIFIED BY tiger;
```

새로 생성한 use1 유져로 오라클에 접속을 하겠습니다.  
```
SQL> conn user1/tiger
```

하지만 접속이 되지않습니다. 아직 user1에게 DB에 접속 권한을 주지 않았기 때문입니다.  
이러한 권한은 SYSTEM 권한을 가진 DBA만 수행할수 있습니다.  
SYSTEM 유져로 접속하여 user1에게 **DB접근권한**을 주겠습니다.  
```
SQL> CONN system/비밀번호

SQL> GRANT CREATE SESSION TO user1;
SQL> CONN user1/tiger;
```

user1 유져로 DB 접속하실수 있습니다.  
다음으로 EMP 테이블를 데이터를 검색해 보겠습니다.  
```
SQL> SELECT * FROM EMP;
```

질의 결과로  "ORA-00942: 테이블 또는 뷰가 존재하지 않습니다."의 결과를 받을겁니다.  
이는 user1에게 해당 테이블 객체의 검색권한이 없기 때문입니다.  
user1에게 EMP 테이블 객체의 **검색권한**을 부여하겠습니다.  
(객체권한 부여는 DBA인 SYS, SYSTEM과 해당 테이블의 소유주가 부여할수 있습니다.)  
```
SQL > CONN SCOTT;
SQL > GRANT SELECT ON EMP TO user1;

SQL> SELECT * FROM SCOTT.EMP;
```

**시스템 권한**은 오라클 접속, 테이블이나 뷰, 인덱스를 생성하는 권한을 말합니다.  
이 권한은 DBA인 SYS와 SYSTEM 유져가 부여합니다.
```
SQL> GRANT system_privilege TO user_name;
SQL> GRANT system_privilege TO PUBLIC;
```

- system privilege  

| privilege | explanation |
| :---: | :---: |
| CREATE USER | Grantee can create other Oracle users. |
| DROP USER | Grantee can drop another user. |
| DROP ANY TABLE | Grantee can drop a table in any schema. |
| BACKUP ANY TABLE | Grantee can back up any table in any schema with the export utility. |
| SELECT ANY TABLE | Grantee can query tables, views, or materialized views in any schema. |
| CREATE ANY TABLE | Grantee can create tables in any schema. |
- (user_name 대신 public을 사용하면 모든 사용자에게 해당 시스템 권한을 부여합니다.)

- [ORA-01950 : 테이블 스페이스 'USERS'에 대한 권한이 없습니다 해결](http://zelits.tistory.com/29){:target="_blank"}
```
sql > alter user user1 default tablespace users quota unlimited on users;
```

**객체 권한**은 테이블이나 뷰나 시퀀스나 함수 등과 같은 객체별로 DML문(SELECT, INSERT, DELETE)을 사용할 수 있는 권한을 설정하는 것입니다.
```
SQL> GRANT object_privilege  ON object TO user_name;
```

---

## 시스템/객체 권한종류

1. 데이터베이스 관리자가 가지는 시스템 권한
위 테이블 참고

2. 일반 사용자가 가지는 시스템 권한  

| 권한 | 기능 |
| :---: | :---: |
| CREATE SESSION | 데이터베이스에 접속할 수 있는 권한 |
| CREATE TABLE | 사용자 스키마에서 테이블을 생성할 수 있는 권한 |
| CREATE VIEW | 사용자 스키마에서 뷰를 생성할 수 있는 권한 |
| CREATE SEQUENCE  | 사용자 스키마에서 시퀀스를 생성할 수 있는 권한 |
| CREATE PROCEDURE | 사용자 스키마에서 함수를 생성할 수 있는 권한  |


3. 일반사용자에게 관리자(시스템) 권한 부여
- 일반 사용자에게 시스템 권한 부여할때 WIDH ADMIN OPTION을 붙여주면 그 사용자는 시스템 권한을 다른 사용자에게 부여할 수 있는 권한을 가지게됩니다.
```
SQL> CONN SYSTEM/비밀번호
SQL> CREATE USER user1 IDENTIFIED BY tiger;
SQL> GRANT CREATE SESSION TO user1  WITH ADMIN OPTION;
SQL> CONN user1/tiger
SQL> GRANT CREATE SESSION TO user2;
```
- 위와같이 일반사용자 user1은 user2에게 CREATE SESSION이라는 시스템 권한을 부여할 수 있습니다.

4. 권한 조회
- user_tab_privs_made : 현재 사용자가 다른 사용자에게 부여한 권한정보를 확인할 수 있습니다.
- user_tab_privs_recd : 현재 사용자에게 부여된 권한정보를 확인할 수 있습니다.
```
SQL> SELECT * FROM user_tab_privs_made; 
SQL> SELECT * FROM user_tab_privs_recd;
```

5. 권한 뺏기/삭제/철회
- 사용자에게 부여된 객체 권한을 데이터베이스 관리자(DBA)나 객체 소유자(OWNER)가 뺏을수 있습니다.
```
SQL> REVOKE object_privilege  ON object FROM user_name;
-- 예
SQL> REVOKE SELECT ON emp FROM user1;
```

6. WITH GRANT OPTION
- 사용자에게 객체 권한을 WITH GRANT OPTION과 함께 부여하면 그 사용자는 그 객체를 접근할 권한을 부여 받으면서 그 권한을 다른 사용자에게 부여할 수 있는 권한도 함께 부여받게 됩니다.
```
SQL> CONN  SCOTT/TIGER
SQL> GRANT SELECT ON SCOTT.emp to user1 WITH GRANT OPTION;
SQL> CONN  person01/tiger; 
SQL> GRANT SELECT ON SCOTT.emp to user2;
```
