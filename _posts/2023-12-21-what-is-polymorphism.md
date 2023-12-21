---
layout: post
title: Java - 다형성이란?
subtitle: 김영한님의 Java 강의로 기초다지기 - 다형성이란?
date: 2023-12-21
author: Warner
header-img: img/bg/post-bg-genetic.jpg
catalog: true
tags:
  - Java
---

## 다형성

객체지향 프로그래밍의 대표적인 특징으로는 캡슐화, 상속, 다형성이 있다. 그 중에서 다형성은 객체지향 프로그래밍의 꽃이라 불린다.\

다형성(Polymorphism)은 이름 그대로 "다양한 형태", "여러 형태"를 뜻한다.\
프로그래밍에서 다형성은 한 객체가 여러 타입의 객체로 취급될 수 있는 능력을 뜻한다. 보통 하나의 객체는 하나의 타입으로 고정되어 있다. 그런데 다형성을 사용하면 하나의 객체가 다른 타입으로 사용될 수 있다는
뜻이다.

다형성을 이해하기 위해서는 크게 2가지 핵심 이론을 알아야 한다.

- 다형적 참조
- 메서드 오버라이딩

## 다형적 참조

![poly1.png](..%2Fimg%2Fpost%2F2023-12-21%2Fpoly1.png)

![poly2.png](..%2Fimg%2Fpost%2F2023-12-21%2Fpoly2.png)

- 부모 타입의 변수가 부모 인스턴스를 참조한다.
- `Parent parent = new Parent()`
- `Parent` 인스턴스를 만들었다. 이 경우 부모 타입인 `Parent`를 생성했기 때문에 메모리 상에 `Parent`만 생성된다.(자식은 생성되지 않는다)
- 생성된 참조값을 `Parent` 타입의 변수인 `Parent`에 담아둔다
- `parent.parentMethod()`를 호출하면 인스턴스의 `Parent` 클래스에 있는 `parentMethod()` 가 호출된다.

![poly3.png](..%2Fimg%2Fpost%2F2023-12-21%2Fpoly3.png)

- 자식 타입의 변수가 자식 인스턴스를 참조한다.
- `Child child = new Child()`
- `Child` 인스턴스를 만들었다. 이 경우 자식 타입인 `Child`를 생성했기 때문에 메머리 상에 `Child`와 `Parent`가 모두 생성된다.
- 생성된 참조값을 `Child` 타입의 변수인 `child`에 담아둔다.
- `child.childMethod()`를 호출하면 인스턴스의 `Child` 클래스에 있는 `childMethod()`가 호출된다.

![poly4.png](..%2Fimg%2Fpost%2F2023-12-21%2Fpoly4.png)

- 부모 타입의 변수가 자식 인스턴스를 참조한다.
- `Parent poly = new Child()`
- `Child` 인스턴스를 만들었다. 이 경우 자식 타입인 `Child`를 생성했기 때문에 메모리 상에 `Child`와 `Parent`가 모두 생성된다.
- 생성된 참조값을 `Parent` 타입의 변수인 `poly`에 담아둔다.

**부모는 자식을 담을 수 있다.**

- 부모 타입은 자식 타입을 담을 수 있다.
- `Parent poly` 는 부모 타입이다. `new Child()`를 통해 생성된 결과는 `Child` 타입이다. 자바에서 부모 타입은 자식 타입을 담을 수 있다!
    - `Parent poly = new Child()`: 성공
- 반대로 자식 타입은 부모 타입을 담을 수 없다.
    - `Child child1 = new Parent()`: 컴파일 오류 발생

![poly5.png](..%2Fimg%2Fpost%2F2023-12-21%2Fpoly5.png)
`Parent poly = new Child()` 이렇게 자식을 참조한 상황에서 `poly` 가 자식 타입인 `Child` 에 있는 `childMethod()` 를 호출하면 어떻게 될까?

- 컴파일 오류 발생

이런 경우 `childMethod()`를 호출하고 싶으면 어떻게 해야할까? 바로 캐스팅이 필요하다.

