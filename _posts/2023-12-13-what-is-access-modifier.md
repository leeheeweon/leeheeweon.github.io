---
layout: post
title: Java - 접근제어자란 무엇인가?
subtitle: 김영한님의 Java 강의로 기초다지기 - 접근제어자란?
date: 2023-12-12
author: Warner
header-img: img/bg/post-bg-access.jpg
catalog: true
tags:
  - Java
---

## 접근제어자

자바는 `public`,`private` 같은 접근 제어자(access modifier)를 제공한다. 접근 제어자를 사용하면 해당 클래스 외부에서 특정 필드나 메서드에 접근하는 것을 허용하거나 제한할 수 있다.
![speaker.png](..%2Fimg%2Fpost%2F2023-12-13%2Fspeaker.png)

`Speaker` 객체를 사용하는 사용자는 `Speaker`의 `volume` 필드와 메서드에 모두 접근할 수 있다.\
`volumeUp()` 메서드가 있지만 소용이 없다 `volume`필드에 직접 접근해서 원하는 값을 설정할 수 있기 때문이다.

이런 문제를 근본적으로 해결하기 위해서는 `volume` 필드의 외부 접근을 막을 수 있는 방법이 필요하다.

![speaker2.png](..%2Fimg%2Fpost%2F2023-12-13%2Fspeaker2.png)
그림을 보면 `volume` 필드를 `private` 을 사용해서 `Speaker` 내부에 숨겼다.\
외부에서 `volume` 필드에 직접 접근할 수 없게 막은 것이다. `volume` 필드는 이제 `Speaker` 내부에서만 접근할 수 있다.

> **참고**: 좋은 프로그램은 무한한 자유도가 주어지는 프로그램이 아니라 적절한 제약을 제공하는 프로그램이다.

## 접근 제어자의 종류