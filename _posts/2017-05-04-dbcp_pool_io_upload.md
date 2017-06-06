---
layout: post
title: tomcat DBCP, POOL, IO, UPLOAD 설정 (우분투)
category: etc
---

## DBCP, POOL 설정

[참고 블로그](http://gangzzang.tistory.com/entry/%ED%86%B0%EC%BA%A3Tomcat-%EC%BB%A4%EB%84%A5%EC%85%98%ED%92%80DBCP-%EC%84%A4%EC%A0%95){:target="_blank"}
- 이전버전 commons-dbcp-1.4jar, commons-pool-1.6.jar, commons-collections-3.2.1-bin.zip 3개의 라이브러리는 톰캣 6.0 부터 tomcat-dbcp.jar 파일로 하나로 통합되었다.
- tomcat-dbcp.jar는 tomcat/lib내에 위치
- tomcat-dbcp.jar를 실행하고 /org/apache/tomcat/dbcp/로 들어가면, pool2, dvcp2가 있음을 확인할 수 있다.
- apache에서 dbcp, pool을 다운 받을 필요가 없다.

---

설정
1. 자신의 프로젝트 이름(dynamic web project) - 우클릭 - properties - java build path
  1. add external jars
    1. mysql-connector-java.jar (위치: /usr/share/java)
    2. servlet-api.jar (위치: /usr/local/tomcat/lib)
2. WebContent - WEB-INF - lib
  1. 우클릭 - import
    1. mysql.jar (위치: /usr/share/java)
    2. servlet-api.jar (위치: /usr/local/tomcat/lib)
    3. tomcat-dbcp.jar (위치: /usr/local/tomcat/lib)
3. WebContent - META-INF - Context.xml
  1. name="jdbc/myconn"에서 myconn은 임의의 문자가 와도 상관없다. 
    1. web.xml의 <res-ref-name>jdbc/myconn</res-ref-name>,
    2. 서블릿의 (DataSource)context.lookup("java:comp/env/jdbc/myconn");
    3. 부분이 일치하기만 하면 됨
    4. acorn은 DB이름 (mysql에서 use acorn;을 먼저 실행할 것)
    ```
    <?xml version="1.0" encoding="UTF-8"?>
    
    <Context>
        <!-- Resource를 등록하여 웹에서 JNDI로 호출할 이름과 정보를 설정한다-->
        <Resource name="jdbc/myconn" auth="Container" type="javax.sql.DataSource"
                        factory="org.apache.tomcat.dbcp.dbcp2.BasicDataSourceFactory"
                        driverClassName="com.mysql.jdbc.Driver"          
                        url="jdbc:mysql://localhost:3306/acorn?autoReconnect=true"
                        
                        username="root" password="123"
                        maxActive="100" maxIdle="30" maxWait="10000"
                        removeAbandoned="true" removeAbandonedTimeout="60"/>
    </Context>
    ```
4. WebContent - WEB-INF - web.xml
    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://java.sun.com/xml/ns/j2ee" xmlns:web="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd http://java.sun.com/xml/ns/j2ee http://java.sun.com/xml/ns/j2ee/web-app_2_4.xsd" id="WebApp_ID" version="2.4">
      <resource-ref>
        <description>My SQL Resource</description>
        <res-ref-name>jdbc/myconn</res-ref-name>
        <res-type>javax.sql.DataSource</res-type>
        <res-auth>Container</res-auth>
      </resource-ref>
      
      <welcome-file-list>
        <welcome-file>Register.html</welcome-file>
      </welcome-file-list>
      
      <servlet>
        <servlet-name>n11</servlet-name>
        <servlet-class>DBCP.dbcplet</servlet-class>
      </servlet>
      <servlet-mapping>
        <servlet-name>n11</servlet-name>
        <url-pattern>/regpro</url-pattern>
      </servlet-mapping>  
    </web-app>
    ```
5. Project Explorer(자신의 프로젝트리스트가 있는 탭)의 아래쪽에 Servers 클릭
  1. META-INF - Context.xml의 내용을 Servers - Tomcat v8.5 Server at localhost-config - context.xml에 붙여넣는다.
    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <!--
      Licensed to the Apache Software Foundation (ASF) under one or more
      contributor license agreements.  See the NOTICE file distributed with
      this work for additional information regarding copyright ownership.
      The ASF licenses this file to You under the Apache License, Version 2.0
      (the "License"); you may not use this file except in compliance with
      the License.  You may obtain a copy of the License at
    
          http://www.apache.org/licenses/LICENSE-2.0
    
      Unless required by applicable law or agreed to in writing, software
      distributed under the License is distributed on an "AS IS" BASIS,
      WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
      See the License for the specific language governing permissions and
      limitations under the License.
    --><!-- The contents of this file will be loaded for each web application -->
    <Context>
    
        <!-- Default set of monitored resources. If one of these changes, the    -->
        <!-- web application will be reloaded.                                   -->
        <WatchedResource>WEB-INF/web.xml</WatchedResource>
        <WatchedResource>${catalina.base}/conf/web.xml</WatchedResource>
    
        <!-- Uncomment this to disable session persistence across Tomcat restarts -->
        <!--
        <Manager pathname="" />
        -->
        <Resource name="jdbc/myconn" auth="Container" type="javax.sql.DataSource"
                        factory="org.apache.tomcat.dbcp.dbcp2.BasicDataSourceFactory"
                        driverClassName="com.mysql.jdbc.Driver"                    
                        url="jdbc:mysql://localhost:3306/acorn?autoReconnect=true"
                        
                        username="root" password="123"
                        maxActive="100" maxIdle="30" maxWait="10000"
                        removeAbandoned="true" removeAbandonedTimeout="60"/>   
    </Context>
    ```
6. terminal
  1. sudo nano /etc/environment
    ```
    CLASSPATH=$CLASSPATH:/usr/local/tomcat/lib/servlet-api.jar:/usr/local/tomcat/lib/jsp-api.jar:/usr/local/tomcat/lib/mysql-connector-java-5.1.38.jar
    ```
    ```
    export CLASSPATH
    ```
7. sudo nano ~/.bashrc는 설정안함
