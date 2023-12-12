---
layout: post
title: Java - 조건문은 무엇인가? 초보자를 위한 이해 가이드
subtitle: 김영한님의 Java 강의로 기초다지기 - 조건문이란?
date: 2023-12-01
author: Warner
header-img: img/bg/post-bg-conditional.png
catalog: true
tags:
  - Java
---

## if문

if 문은 특정 조건이 참인지 확인하고, 그 조건이 참(true)일 경우 특정 코드 블록을 실행한다.

~~~java
public class If1 {
    public static void main(String[] args) {
        int age = 20;

        if (age >= 18) {
            System.out.println("성인입니다.");
        }

        if (age < 18) {
            System.out.println("미성년자입니다.");
        }
    }
}
~~~

## else문

else문은 if문에서 만족하는 조건이 없을 때 실행하는 코드를 제공한다.

~~~java
public class If2 {
    public static void main(String[] args) {
        int age = 20;

        if (age >= 18) {
            System.out.println("성인입니다.");
        } else {
            System.out.println("미성년자입니다.");
        }
    }
}
~~~

## else if문

~~~java
public class If3 {
    public static void main(String[] args) {
        int age = 14;

        if (age <= 7) {
            System.out.println("미취학");
        } else if (age <= 13) {
            System.out.println("초등학생");
        } else if (age <= 16) {
            System.out.println("중학생");
        } else if (age <= 19) {
            System.out.println("고등학생");
        } else {
            System.out.println("성인");
        }
    }
}
~~~

## switch문

~~~java
public class Switch1 {
    public static void main(String[] args) {
        int grade = 2;

        int coupon = 0;
        switch (grade) {
            case 1:
                coupon = 1000;
                break;
            case 2:
                coupon = 2000;
                break;
            case 3:
                coupon = 3000;
                break;
            default:
                coupon = 500;
                break;
        }
        System.out.println("coupon = " + coupon);
    }
}
~~~
