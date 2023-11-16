---
layout: post
title: Spring Session - DB에 세션 저장 방식(JDBC)
subtitle: 스프링 세션 jdbc
date: 2023-11-16
author: Warner
header-img: img/bg/post-bg-earth.jpg
catalog: true
tags:
  - Spring
---
## 스프링 세션 동작 방식 
- 서버에 로그인 세션을 저장하는 방식으로 구현(기존 동작 방식)
- WAS의 메모리에서 저장되고 호출
- 스프링부트와 같이 내장 톰캣(WAS)를 사용하는 경우, 재실행시 WAS의 메모리 초기화, 세션정보 유지X
- 2대 이상의 WAS가 구동되면 **톰캣 간에 세션 정보를 공유**해야 함

## 스프링 세션 저장 방법
1. MySql 등의 DB를 세션 저장소로 사용
   - 로그인 요청이 잦을 경우, 로그인 세션을 확인할때마다 DB에 접근해야 하므로 **성능 문제가 발생할 수 있음**. 
2. Redis 등 인메모리 DB를 세션 저장소로 사용

## Gradle 추가 
~~~java
dependencies {
        implementation 'org.springframework.session:spring-session-jdbc'
        implementation 'mysql:mysql-connector-java'
        }
~~~


## DB 접속 정보 입력
~~~yaml
spring:
  datasource:
    url: jdbc:mysql://[DB IP 주소]:[DB 포트]/[DB 이름]?useSSL=false
    username: [DB 계정 이름]
    password: [DB 계정 비밀번호]
~~~

## 설정 추가 
~~~ yaml
spring:
  session:
    jdbc:
      initialize-schema: always
~~~

이 설정을 추가하고 애플리케이션을 실행하면 SPRING_SESSION 테이블이 자동으로 생성되어 세션 정보를 저장할 수 있게 됩니다.