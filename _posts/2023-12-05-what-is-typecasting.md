---
layout: post
title: Java - What is Type casting? (형변환이란?)
subtitle: 김영한님의 Java 강의로 기초다지기 - 형변환이란?
date: 2023-12-05
author: Warner
header-img: img/bg/post-bg-compare.jpg
catalog: true
tags:
  - Java
---

## 자동 형변환

- 작은 범위에서 큰 범위로는 당연히 값을 넣을 수 있다.
    - 예) int -> long -> double
- 큰 범위에서 작은 범위는 다음과 같은 문제가 발생할 수 있다.
    - 소수점 버림
    - 오버플로우

~~~java
public class Casting1 {
    public static void main(String[] args) {
        int intValue = 10;
        long longValue;
        double doubleValue;

        longValue = intValue; // int -> long
        System.out.println("longValue = " + longValue);

        doubleValue = intValue; // int -> double
        System.out.println("doubleValue = " + doubleValue);

        doubleValue = 20L; // long -> double
        System.out.println("doubleValue2 = " + doubleValue);
    }
}
~~~

작은 범위 숫자 타입에서 큰 범위 숫자 타입으로의 대입은 개발자가 이렇게 직접 형변환을 하지 않아도 된다.
이런 과정이 자동으로 일어나기 때문에 **자동 형변환**, 또는 **묵시적 형변환** 이라고 한다.

## 명시적 형변환

큰 범위에서 작은 범위 대입은 명시적 형변환이 필요하다.

~~~java
public class Casting2 {
    public static void main(String[] args) {
        double doubleValue = 1.5;
        int intValue = 0;

//        intValue = doubleValue;  //컴파일 오류 발생
        intValue = (int) doubleValue;
        System.out.println("intValue = " + intValue);
    }
}
~~~

**형변환**

데이터 타입을 강제로 변경할 수 있다.

형변환은 다음과 같이 변경하고 싶은 데이터 타입을 (int) 와 같이 괄호를 사용해서 명시적으로 입력하면 된다.

intValue = (int) doubleValue;

이것을 형(타입)을 바꾼다고 해서 형변환이라 한다. 영어로는 캐스팅이라 한다. 그리고 개발자가 직접 형변환 코드를 입력한다고 해서 **명시적 형변환**이라 한다.

**캐스팅 용어**
"캐스팅"은 영어 단어 "cast"에서 유래되었다. "cast"는 금속이나 다른 물질을 녹여서 특정한 형태나 모양으로 만드는 과정을 의미한다.

## 형변환과 오버플로우

~~~java
public class Casting3 {
    public static void main(String[] args) {
        long maxIntValue = 2147483647; //int 최고값
        long maxIntOver = 2147483648L; //int 최고값 + 1 (초과)

        int intValue = 0;
        intValue = (int) maxIntValue; //형변환
        System.out.println("intValue = " + intValue);

        intValue = (int) maxIntOver; //형변환
        System.out.println("intValue = " + intValue); //intValue = -2147483648
    }
}
~~~

정상 범위는 문제가 없다
초과 범위는 마치 시계가 한바퀴 돈 것 처럼 다시 처음부터 시작한다.

## 계산과 형변환 
~~~java
public class Casting4 {
    public static void main(String[] args) {
        int div1 = 3 / 2;
        System.out.println("div1 = " + div1); // 1

        double div2 = 3 / 2;
        System.out.println("div2 = " + div2); // 1.0

        double div3 = 3.0 / 2;
        System.out.println("div3 = " + div3); // 1.5

        double div4 = (double) 3 / 2;
        System.out.println("div4 = " + div4); // 1.5

        int a = 3;
        int b = 2;
        double result = (double) a / b;
        System.out.println("result = " + result);
    }
}
~~~
1. 같은 타입끼리의 계산은 같은 타입의 결과를 낸다.
2. 서로 다른 타입의 계산은 큰 범위로 자동 형변환이 일어난다.