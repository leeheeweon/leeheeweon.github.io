---
layout: post
title: Java - 코드 블록이란? 초보자를 위한 이해 가이드
subtitle: 김영한님의 Java 강의로 기초다지기 - 스코프란?
date: 2023-12-05
author: Warner
header-img: img/bg/post-bg-blocks.jpg
catalog: true
tags:
  - Java
---

## 지역 변수와 스코프

변수는 선언한 위치에 따라 지역 변수, 멤버 변수(클래스 변수, 인스턴스 변수)와 같이 분류된다.

지역변수(Local Variable)는 이름 그대로 특정 지역에서만 사용할 수 있는 변수라는 뜻이다.
그 특정 지역을 벗어나면 사용할 수 없다.\
여기서 말하는 지역이 바로 변수가 선언된 **코드 블록({})** 이다.\
지역 변수는 자신이 선언된 **코드 블록({})** 안에서만 생존하고, 자신이 선언된 코드 블록을 벗어나면 제거된다.

~~~java
public class Scope1 {
    public static void main(String[] args) {
        int m = 10; //m 생존 시작

        if (true) {
            int x = 20; //x 생존 시작
            System.out.println("m = " + m);
            System.out.println("x = " + x);
        } //x 생존 종료
//        System.out.println("x = " + x);
        System.out.println("m = " + m);
    } //m 생존 종료
}
~~~

### 스코프 존재 이유

~~~java
public class Scope3_1 {
    public static void main(String[] args) {
        int m = 10;
        int temp = 0;

        if (m > 0) {
            temp = m * 2;
            System.out.println("temp = " + temp);
        }

        System.out.println("m = " + m);
    }
}
~~~

변수 temp는 if문 안에서만 사용하기 때문에 if문 안으로 들어가도록 리팩토링 해야한다.

스코프가 없다면 아래와 같은 문제가 발생
- 비효율적인 메모리 사용 : 변수 템프를 if 코드 블록 안으로 이동시키면 if 코드 블록이 종료 시점에 이 변수를 메모리에서 제거해서 더 효율적으로 메모리를 사용할 수 있다.
- 코드 복잡성 증가 : 좋은 코드는 군더더기 없는 단순한 코드이다. temp가 if 코드 블록 안에 있다면 코드 블록이 끝나는 시점에서 temp는 더이상 생각하지 않아도 된다. 

## 정리 
- 변수는 꼭 필요한 범위로 한정해서 사용하는 것이 좋다. 변수의 스코프는 꼭 필요한 곳으로 한정해서 사용하자. 메모리를 효율적으로 사용하고 더 유지보수하기 좋은 코드를 만들 수 있다.
- **좋은 프로그램은 무한한 자유가 있는 프로그램이 아니라 적절한 제약이 있는 프로그램이다.**