---
layout: post
title: Java - Object 다형성이란?
subtitle: 김영한님의 Java 강의로 기초다지기 - Object 다형성이란?
date: 2024-04-17
author: Warner
header-img: img/bg/post-bg-object2.jpg
catalog: true
tags:
  - Java
---

## Object 다형성 
`Object`는 모든 클래스의 부모 클래스이다. 따라서 `Object`는 모든 객체를 참조할 수 있다.
![object2.png](/img/post/2024/2024-04-17/object2.png)

`Dog`와 `Car`은 서로 아무런 관련이 없는 클래스이다. 둘다 부모가 없으므로 `Object`를 자동으로 상속 받는다.

**Object를 활용한 다형성의 한계**
- `Object`는 모든 객체를 대상으로 다형적 참조를 할 수 있다.
  - 쉽게 이야기해서 `Object`는 모든 객체의 부모이므로 모든 객체를 담을 수 있다.
- `Object`를 통해 전달 받은 객체를 호출하려면 각 객체에 맞는 다운캐스팅 과정이 필요하다.
  - `Object`가 세상의 모든 메서드를 알고 있는 것은 아니다.

다형성을 제대로 활용하려면 다형적 참조 + 메서드 오버라이딩을 함께 사용해야 한다. 그런면에서 `Object`를 사용한 다형성에는 한계가 있다.\
`Object`는 모든 객체의 부모이므로 모든 객체를 대상으로 다형적 참조를 할 수 있다. 하지만 Object에는 Dog.sound(), Car.move()와 같은 다른 객체의 메서드가 정의되어 있지 않다.
따라서 메서드 오버라이딩을 활용할 수 없다. 결국 각 객체의 기능을 호출하려면 다운캐스팅을 해야 한다.\
참고로 `Object` 본인이 보유한 `toString()` 같은 메서드는 당연히 자식 클래스에서 오버라이딩 할 수 있다. 여기서 이야기하는 것은 앞서 설명한 `Dog.sound()`, `Car.move()` 같은 `Object`에 속하지 않은 메서드를 말한다.

