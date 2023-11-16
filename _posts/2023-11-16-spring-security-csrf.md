---
layout: post
title: Spring Security - 크로스 사이트 요청 위조(CSRF)
subtitle: 크로스 사이트 요청 위조(CSRF)
date: 2023-11-16
author: Warner
header-img: img/bg/post-bg-hacker.jpg
catalog: true
tags:
  - Spring
---

## 크로스 사이트 요청 위조(CSRF)란?

- 사용자 의지와 무관하게 공격자의 의도대로 서버에 특정 요청을 하도록 함

## CSRF 공격 사례

> 사례1) A 게시글에서 사진을 클릭 했는데 나도 모르게 B 게시글에 좋아요가 눌렸다.
>
> 사례2) id가 1111인 게시글에 이미지 태그를 삽입하여 src 값에 "http://community.com/like?post=2222" id가 2222인 게시글의 조회수도 함께 올라갔다.

## CSRF 언제 사용 하는가?

> When to use CSRF protectionWhen should you use CSRF protection? Our recommendation is to use CSRF protection for any
> request that could be processed by a browser by normal users. If you are creating a service that is used only by
> non-browser clients, you likely want to disable CSRF protection.

우리는 일반 사용자가 브라우저에서 처리할 수 있는 모든 요청에 대해 CSRF 보호를 사용하는 것을 권장합니다. **브라우저가 아닌 클라이언트**에서만 사용되는 서비스를 생성하는 경우 **CSRF 보호를 비활성화**할
수 있습니다.

**즉 REST API 서버 기준으로 disable을 진행**

## CSRF 보호 구성 요소 이해

![csrf1.png]( /img/post/2023-11-16/csrf1.png)

CSRF 보호는 두 부분으로 나누어진다.

1. CsrfToken에 위임하여 애플리케이션에서 을 사용, CsrfTokenRequestHandler.
2. 요청에 CSRF 보호가 필요한지 확인하고 토큰을 로드 및 검증한 후AccessDeniedException .

![csrf-processing.png]( /img/post/2023-11-16/csrf-processing.png)

## CSRF Token

### Default
Spring Security는 POST 요청과 같은 안전하지 않은 HTTP 메서드 에 대해 기본적으로 CSRF 공격으로부터 보호 하므로 **추가 코드가 필요X** 

다음을 사용하여 기본 구성을 명시적으로 지정할 수 있다.

~~~java
@Configuration
@EnableWebSecurity
public class SecurityConfig {

	@Bean
	public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
		http
			// ...
			.csrf(Customizer.withDefaults());
		return http.build();
	}
}
~~~

### HttpSessionCsrfTokenRepository

기본적으로 Spring Security는 를 HttpSession사용하여 예상되는 CSRF 토큰을 저장 HttpSessionCsrfTokenRepository하므로 추가 코드가 필요X.

~~~java
@Configuration
@EnableWebSecurity
public class SecurityConfig {

	@Bean
	public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
		http
			// ...
			.csrf((csrf) -> csrf
				.csrfTokenRepository(new HttpSessionCsrfTokenRepository())
			);
		return http.build();
	}
}
~~~


HTTP 요청 헤더 또는 요청 매개변수 HttpSessionCsrfTokenRepository에서 토큰을 확인 . \
X-CSRF-TOKEN_csrf
![csrf-token.png]( /img/post/2023-11-16/csrf-token.png)

## CSRF TOKEN 자동 포함 
- Spring’s form tag library(스프링 폼태그 라이브러리)
- Thymeleaf(타임리프)
- Any other view technology that integrates with RequestDataValueProcessor (via CsrfRequestDataValueProcessor) (기타 뷰)
- You can also include the token yourself via the csrfInput tag(csrf 태그를 통해 직접 포함 가능)


## CSRF TOKEN 직접 포함 방법

### FORM 태그
~~~html
<input type="hidden"
       name="${_csrf.parameterName}"
       value="${_csrf.token}"/>
~~~

### META 태그
~~~html
<html>
<head>
	<meta name="_csrf" content="${_csrf.token}"/>
	<!-- default header name is X-CSRF-TOKEN -->
	<meta name="_csrf_header" content="${_csrf.headerName}"/>
	<!-- ... -->
</head>
<!-- ... -->
</html>
~~~

### AJAX 요청 
~~~javascript
$(function () {
	var token = $("meta[name='_csrf']").attr("content");
	var header = $("meta[name='_csrf_header']").attr("content");
	$(document).ajaxSend(function(e, xhr, options) {
		xhr.setRequestHeader(header, token);
	});
});
~~~