---
layout: post
title: Spring Security - 스프링 시큐리티란?
subtitle: 스프링 시큐리티 이론 정리
date: 2023-11-20
author: Warner
header-img: img/bg/post-bg-hacker.jpg
catalog: true
tags:
  - Spring
---

## 스프링 시큐리티란?

Spring security는 인증, 권한 부여 및 일반적인 공격에 대한 보호를 제공하는 프레임 워크이다.

## Gradle로 시작하기

Spring Boot는 spring-boot-starter-security Spring Security 관련 종속성을 집계하는 스타터 제공

~~~yaml
dependencies {
  implementation "org.springframework.boot:spring-boot-starter-security"
}
~~~

## 특징

Spring Security는 **인증, 권한 부여 및 일반적인 악용**에 대한 보호를 위한 포괄적인 지원을 제공

## 아키텍쳐

![multi-securityfilterchain.png](..%2Fimg%2Fpost%2F2023-11-20%2Fmulti-securityfilterchain.png)

1. 필터검토
2. 필터프록시 위임
3. 필터체인프록시
4. 보안필터체인

## Config

보안 필터는 **SecurityFilterChain API**를 사용하여 **FilterChainPorxy**에 삽입된다.

~~~ java
자바
@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .csrf(Customizer.withDefaults())
            .authorizeHttpRequests(authorize -> authorize
                .anyRequest().authenticated()
            )
            .httpBasic(Customizer.withDefaults())
            .formLogin(Customizer.withDefaults());
        return http.build();
    }

}
~~~

위 설정의 구성 순서

| Filter                               | Added By                           |
|--------------------------------------|------------------------------------|
| CsrfFilter                           | HttpSecurity#csrf                  |
| UsernamePasswordAuthenticationFilter | HttpSecurity#formLogin             |
| BasicAuthenticationFilter            | HttpSecurity#httpBasic             |
| AuthorizationFilter                  | HttpSecurity#authorizeHttpRequests |