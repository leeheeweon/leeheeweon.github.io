---
layout: post
title: JWT - JSON Web Token
subtitle: JWT 사용을 위한 개념 정리
date: 2023-11-27
author: Warner
header-img: img/bg/post-bg-jwt.png
catalog: true
tags:
  - JWT
---

## JWT (JSON Web Token) 이란?

JWT는 JSON Web Token 의 약자로 전자 서명 된 URL-safe의 JSON 이다.

## JWT를 언제 사용해야 하는가?

- 승인 : 사용자가 로그인하면 각 후속 요청에 JWT가 포함되어 사용자가 해당 토큰을로 허용되는 경로, 서비스 및 리소스에 액세스 할 수 있다.


- 정보교환 : JWT는 당사자 간에 정보를 안전하게 전송하는 좋은 방법이다.\
  예를 들어 공개/개인 키 쌍을 사용하여 JWT에 서명할 수 있어 보낸 사람이 누구인지 확인할 수 있다.\
  또한 헤더와 페이로드를 사용해 서명을 계산하므로 콘텐츠 변조 여부를 확인할 수 있다.

## JWT 구조

점(.)으로 구분된 세 부분으로 구성

- 헤더
- 페이로드
- 시그니처

~~~yaml
xxxxx.yyyyy.zzzzz
~~~

### 헤더

헤더는 일반적으로 토큰 유형(JWT)과 사용되는 서명 알고리즘(HMAC, SHA256, RSA)으로 구성

헤더 예시

~~~json
{
  "alg": "HS256",
  "typ": "JWT"
}
~~~

### 페이로드

토큰의 두 번째 부분은 **클레임(claims)** 을 포함하는 페이로드이다.\
클레임은 엔티티 및 추가 데이터에 대한 설명이다.\
클레임은 **registerd, public, private** 3가지로 구분된다.

- Registered claims : 권장하는 클레임 집합이다.
    - iss(issur)
    - exp(expiration time)
    - sub(subject)
    - aud(audience)

- Public claims : 정의하여 사용가능, 충돌방지를 위해 [IANA JSON Web Token Registry](https://www.iana.org/assignments/jwt/jwt.xhtml)
  정의하거나 URL에 충돌방지 네임스페이스를 포함하여 정의해야 한다.


- Private claims : 사용에 동의한 당사자 간에 정보를 공유하기 위해 생성된 맞춤 클레임이다.

페이로드 예시

~~~json
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
~~~

### 시그니처

시그니처를 생성하려면 헤더에 지정된 알고리즘을 만들고 알고리즘에 인코딩된 헤더, 인코딩된 페이로드, 비밀을 포함해야 한다.

시그니처는 메시지가 도중에 변경되지 않았는지 확인하는데 사용,
개인키로 시그니처된 경우 JWT의 보낸 사람이 누구인지 확인할 수 있다.

시그니처 예시

~~~js
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
~~~

## JWT의 Access Token / Refresh Token

제 3자에게 토큰 탈취의 위험성이 있으므로 Access Token, Refresh Token으로 나누어 인증한다.

Access Token 과 Refresh Token은 둘다 JWT 이다. 토큰이 어디에 저장되고 관리되느냐에 따른 사용 차이가 있다.

- Access Token : 클라이언트가 갖고있는 실제로 유저의 정보가 담긴 토큰, 클라이언트에서 요청이 오면 서버에서 해당 토큰에 있는 정보를 활용하여 사용자 정보에 맞게 응답을 진행


- Refresh Token : 새로운 Access Token을 발급해주기 위해 사용하는 토큰, 해당 토큰은 데이터베이스에 유저 정보와 같이 기록.

## 요약

JWT 는 Base64로 암호화를 하기 때문에 디버거를 사용해서 인코딩된 JWT를 복호화 가능하다.\
복호화시 사용자 데이터가 노출되기 때문에 민감한 정보는 배제해야 한다.\
그럼 JWT의 진짜 목적은 무엇일까?\
JWT의 목적은 **정보 보호가 아닌, 위조 방지** 이다.

