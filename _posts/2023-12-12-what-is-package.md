---
layout: post
title: Java - 패키지는 무엇인가? 초보자를 위한 이해 가이드
subtitle: 김영한님의 Java 강의로 기초다지기 - 패키지란?
date: 2023-12-12
author: Warner
header-img: img/bg/post-bg-package.jpg
catalog: true
tags:
  - Java
---

## 패키지 - 시작

쇼핑몰 시스템을 개발한다고 가정해보자. 다음과 같이 프로그램이 매우 작고 단순해서 클래스가 몇개 없다면 크게 고민할 거리가 없겠지만, 기능이 점점 추가되어서 프로그램이 아주 커지게 된다면 어떻게 될까?

**아주 작은 프로그램**

~~~text
Order
User
Product
~~~

**큰 프로그램**

~~~text
User
UserManager
UserHistory
Product
ProductCatalog
ProductImage
Order
OrderService
OrderHistory
ShoppingCart
CartItem
Payment
PaymentHistory
Shipment
ShipmentTracker
~~~

컴퓨터는 보통 파일을 분류하기 위해 폴더, 디렉토리라는 개념을 제공한다. 자바도 이런 개념을 제공하는데, 이것이 바로 패키지이다.

~~~text
* user
 * User
 * UserManager
 * UserHistory
* product
 * Product
 * ProductCatalog
 * ProductImage
* order
 * Order
 * OrderService
 * OrderHistory
* cart
 * ShoppingCart
 * CartItem
* payment
 * Payment
 * PaymentHistory
* shipping
 * Shipment
 * ShipmentTracker
~~~

여기서 `user, product` 등이 바로 패키지이다. 그리고 해당 패키지 안에 관련된 자바 클래스들을 넣으면 된다.\
패키지(`package`)는 이름 그대로 물건을 운송하기 위한 포장 용기나 그 포장 묶음을 뜻한다.

## 패키지 사용

~~~java
package pack;

public class Data {
    public Data() {
        System.out.println("패키지 pack Data 생성");
    }
}
~~~

- **패키지를 사용하는 경우 항상 코드 첫줄에 `package pack`과 같이 패키지 이름을 적어주어야 한다.**


- **사용자와 같은 위치**: 같은 패키지에 있는 경우에는 패키지 경로를 생략해도 된다.
- **사용자와 다른 위치**: 패키지가 다르면 패키지 전체 경로를 포함해서 클래스를 적어주어야 한다.

## 패키지 - import

패키지 전체 경로를 포함해서 클래스를 적어주는 것은 불편하다. 이때는 `import`를 사용하면 된다.

코드에서 첫줄에는 `package`를 사용하고, 다음 줄에는 `import`를 사용할 수 있다.\
`import`를 사용하면 다른 패키지에 있는 클래스를 가져와서 사용할 수 있다.\
`import`를 사용한 덕분에 코드에서는 패키지 명을 생략하고 클래스 이름만 적을 수 있다.

> 특정 패키지에 포함된 모든 클래스를 포함해서 사용하고 싶으면 `import` 시점에 `*(별)`을 사용하면 된다.

## 패키지 규칙

- 패키지의 이름과 위치는 폴더(디렉토리) 위치와 같아야 한다.(필수)
- 패키지 이름은 모두 소문자를 사용한다.(관례)
- 패키지 이름의 앞 부분에는 일반적으로 회사의 도메인 이름을 거꾸로 사용한다. 예를 들어, `com.company.myapp`과 같이 사용한다.(관례)
    - 이 부분은 필수는 아니다. 하지만 수 많은 외부 라이브러리가 함께 사용되면 같은 패키지에 같은 클래스 이름이 존재할 수도 있다. 이렇게 도메인 이름을 거꾸로 사용하면 이런 문제를 방지할 수 있다.
    - 내가 오픈소스나 라이브러리를 만들어서 외부에 제공한다면 꼭 지키는 것이 좋다.
    - 내가 만든 애플리케이션을 다른 곳에 공유하지 않고, 직접 배포한다면 보통 문제가 되지 않는다.
