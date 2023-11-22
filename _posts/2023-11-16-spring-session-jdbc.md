---
layout: post
title: Spring Session - DB에 세션 저장 방식(JDBC)
subtitle: 스프링 세션 jdbc
date: 2023-11-16
author: Warner
header-img: img/bg/post-bg-earth.png
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
dependencies{
        implementation'org.springframework.session:spring-session-jdbc'
        implementation'mysql:mysql-connector-java'
        }
~~~

## DB 접속 정보 입력

~~~yaml
spring:
  datasource:
    url: jdbc:mysql://[DB IP 주소]:[DB 포트]/[DB 이름]?useSSL=false
    username: [ DB 계정 이름 ]
    password: [ DB 계정 비밀번호 ]
~~~

## 설정 추가

~~~ yaml
spring:
  session:
    jdbc:
      initialize-schema: always
~~~

이 설정을 추가하고 애플리케이션을 실행하면 SPRING_SESSION 테이블이 자동으로 생성되어 세션 정보를 저장할 수 있게 됩니다.

## 객체 직렬화

~~~java
public class Member implements Serializable {

}
~~~

- 자바 직렬화란 자바 시스템 내부에서 사용되는 객체 또는 데이터를 외부의 자바 시스템에서도 사용할 수 있도록 바이트(byte) 형태로 데이터 변환하는 기술과 바이트로 변환된 데이터를 다시 객체로 변환하는 기술(역
  직렬화)을 아울러서 이야기한다.