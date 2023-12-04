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

## break, continue

break 와 continue는 반복문에서 사용할 수 있는 키워드다.
break 는 반복문을 즉시 종료하고 나간다.
continue 는 반복문의 나머지 부분을 건너뛰고 다음 반복으로 진행하는데 사용된다.

~~~java
public class Break1 {
    public static void main(String[] args) {
        int sum = 0;
        int i = 1;
        while (true) {
            sum += 1;

            if (sum > 10) {
                break;
            }

            System.out.println("sum = " + sum);
            i++;
        }
    }
}
~~~

## for 문

for문도 while문과 같은 반복문이고, 코드를 반복 실행하는 역할을 한다.
for문은 주로 반복 횟수가 정해져 있을 때 사용한다.

~~~java
public class For2 {
    public static void main(String[] args) {
        int sum = 0;
        int endNum = 3;

        for (int i = 1; i <= endNum; i++) {
            sum += i;
            System.out.println("i = " + i + " sum=" + sum);
        }
    }
}
~~~

### for vs while

둘을 비교했을 때 for문이 더 깔끔하다는 느낌을 받을 것이다. for문은 초기화, 조건 검사, 반복 후 작업 등이 규칙적으로 한 줄에 모두 들어있어 코드를 이해하기 더 쉽다.
특히 반복을 위해 값이 증가하는 카운터 변수를 다른 부분과 병확하게 구분할 수 있다.

## 중첩 반복문
반복문은 내부에 또 반복문을 만들 수 있다. for, while 모두 가능하다.

~~~java
public class Nested1 {
    public static void main(String[] args) {
        for (int i = 0; i < 2; i++) {
            System.out.println(" i=시작 " + i);
            for (int j = 0; j < 3; j++) {
                System.out.println("j = " + j);
            }
            System.out.println(" i=종료 " +i);
        }
    }
}
~~~