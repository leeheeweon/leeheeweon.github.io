---
layout: post
title: Java - What is Loop? (반복문이란 무엇인가?)
subtitle: 김영한님의 Java 강의로 기초다지기 - 반복문이란?
date: 2023-12-04
author: Warner
header-img: img/bg/post-bg-java.jpg
catalog: true
tags:
  - Java
---

## 반복문 시작

반복문은 이름 그대로 특정 코드를 반복해서 실행할 때 사용한다.
자바는 다음 3가지 종류의 반복문을 제공한다.

**while, do-while, for**

## while 문

~~~java
public class While1_2 {
    public static void main(String[] args) {
        int count = 0;

        while (count < 3) {
            count++;
            System.out.println("count = " + count);
        }
    }
}
~~~

- while 조건에 만족할때까지 반복

## do-while 문

do-while문은 while문과 비슷하지만, 조건에 상관없이 무조건 한 번은 코드를 실행한다.

~~~java
public class DoWhile2 {
    public static void main(String[] args) {
        int i = 10;

        do {
            System.out.println("i = " + i);
            i++;
        } while (i < 3);
    }
}
~~~

- do while 문 최초 한번 실행, 조건이 참이면 do 부분 반복 실행


## for 문