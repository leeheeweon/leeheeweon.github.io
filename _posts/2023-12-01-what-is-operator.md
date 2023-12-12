---
layout: post
title: Java - 연산자는 무엇인가?
subtitle: 김영한님의 Java 강의로 기초다지기 - 연산자란?
date: 2023-12-01
author: Warner
header-img: img/bg/post-bg-operator.jpg
catalog: true
tags:
  - Java
---

## 연산자의 시작

+, -, *, / 와 같이 계산을 수행하는 기호를 연산자라 한다.

## 연산자의 종류

- 산술 연산자 : =, -, *, /, %
- 증감 연산자 : ++, --
- 비교 연산자 : ==, !=, >, <, >=, <=
- 논리 연산자 : &&, ||, !
- 대입 연산자 : =, +=, -=, *=, /=, %=
- 삼항 연산자 : ? :

## 연산자와 피연산자

~~~ java
3 + 4
a + b
~~~

- 연산자 (operator) : 연산 기호 -예) +, -
- 피연산자 (operand) : 연산 대상 -예) 3, 4, a, b

## 산술 연산자

~~~java
public class Operator1 {
    public static void main(String[] args) {
        int a = 5;
        int b = 2;

        //덧셈
        int sum = a + b;
        System.out.println("sum = " + sum);

        //뺄셈
        int diff = a - b;
        System.out.println("diff = " + diff);

        //곱셈
        int multi = a * b;
        System.out.println("multi = " + multi);

        //나눗셈
        double div = (double) a / b;
        System.out.println("div = " + div);

        //나머지
        int mod = a % b;
        System.out.println("mod = " + mod);
    }
}
~~~

## 문자열 더하기

자바는 문자열에도 + 연산자를 사용할 수 있다.

~~~java
public class Operator2 {
    public static void main(String[] args) {
        //문자열과 문자열 더하기1
        String result1 = "hello" + "world";
        System.out.println("result1 = " + result1);

        //문자열과 문자열 더하기2
        String s1 = "string1";
        String s2 = "string2";
        String result2 = s1 + s2;
        System.out.println("result2 = " + result2);

        //문자열과 숫자 더하기1
        String result3 = "a + b = " + 10;
        System.out.println("result3 = " + result3);

        //문자열과 숫자 더하기2
        int num = 20;
        String str = "a + b = ";
        String result4 = str + num;
        System.out.println("result4 = " + result4);
    }
}
~~~

## 연산자 우선순위

~~~java
public class Operator3 {
    public static void main(String[] args) {
        int sum1 = 1 + 2 * 3;
        int sum2 = (1 + 2) * 3;
        System.out.println("sum1 = " + sum1);
        System.out.println("sum2 = " + sum2);

        int sum3 = 2 * 2 + 3 * 3;
        int sum4 = (2 * 2) + (3 * 3);
        System.out.println("sum3 = " + sum3);
        System.out.println("sum4 = " + sum4);
    }
}
~~~

### 연산자 우선순위 암기법

1. 상식선에서 우선순위를 사용하자
2. 애매하면 괄호()를 사용하자

## 증감 연산자

증가 및 감소 연산자를 증감 연산자라 한다.

~~~java
public class OperatorAdd1 {
    public static void main(String[] args) {
        int a = 0;
        a = a + 1;
        System.out.println("a = " + a); //1

        a += 1;
        System.out.println("a = " + a); //2

        ++a;
        System.out.println("a = " + a); //3
    }
}
~~~

### 전위, 후위 증감연산자

증감 연산자는 피연산자 앞에 두거나 뒤에 둘 수 있으며, 연산자의 위치에 따라 연산이 수행되는 시점이 달라진다.

- ++a : 증감 연산자를 피연산자 앞에 둘 수 있다. 전위(Prefix) 증감 연산자라 한다.
- a++ : 증감 연산자를 피연산자 뒤에 둘 수 있다. 후위(Postfix) 증감 연산자라 한다.

~~~java
public class OperatorAdd2 {
    public static void main(String[] args) {
        //전위 증감 연산자
        int a = 1;
        int b = 0;

        b = ++a;
        System.out.println("a = " + a + "b = " + b); // 결과 a=2 b=2

        // 후위 증감 연산자
        a = 1;
        b = 0;
        b = a++;
        System.out.println("a = " + a + "b = " + b); // 결과 a=2 b=1
    }
}
~~~

## 비교 연산자

비교 연산자는 두 값을 비교하는 데 사용된다.

비교 연산자를 사용하면 참(true) 또는 거짓(false)이라는 결과가 나온다. 참 거짓은 boolean 형을 사용한다.

~~~java
public class Comp1 {
    public static void main(String[] args) {
        int a = 2;
        int b = 3;
        System.out.println(a == b); // false
        System.out.println(a != b); // true
        System.out.println(a > b); // false
        System.out.println(a < b); // true
        System.out.println(a >= b); // false
        System.out.println(a <= b); // true

        boolean result = a == b;
        System.out.println("result = " + result);
    }
}
~~~

### 문자열 비교

문자열이 같은지 비교할 때는 == 이 아니라 .equals() 메서드를 사용해야 한다.

~~~java
public class Comp2 {
    public static void main(String[] args) {
        String str1 = "문자열1";
        String str2 = "문자열2";

        boolean result1 = "hello".equals("hello");
        boolean result2 = str1.equals("문자열1");
        boolean result3 = str1.equals(str2);

        System.out.println("result1 = " + result1); // true
        System.out.println("result2 = " + result2); // true
        System.out.println("result3 = " + result3); // false
    }
}
~~~

## 논리 연산자

논리 연산자는 bollean 형인 true, false를 비교하는데 사용한다.

~~~java
public class Logical1 {
    public static void main(String[] args) {
        System.out.println("&&: AND 연산");
        System.out.println(true && true); //true
        System.out.println(true && false); //false
        System.out.println(false && false); //false

        System.out.println("|| : OR 연산");
        System.out.println(true || true); //true
        System.out.println(true || false); //true
        System.out.println(false || false); //false

        System.out.println("! 연산");
        System.out.println(!true); //false
        System.out.println(!false); //true

        System.out.println("변수 활용");
        boolean a = true;
        boolean b = false;
        System.out.println(a && b); //false
        System.out.println(a || b); //true
        System.out.println(!a); //false
        System.out.println(!b); //true
    }
}
~~~

## 대입 연산자

대입 연산자(=)는 값을 변수에 할당하는 연산자다. 이 연산자를 사용하면 변수에 값을 할당할 수 있다.

### 축약(복합) 대입 연산자

산술 연산자와 대입 연산자를 한번에 축약해서 사용할 수 있는데, 이것을 축약(복합) 대입 연산자라 한다.

연산자 종류: +=, -=, *=, /=, %=

~~~java
public class Assign1 {
    public static void main(String[] args) {
        int a = 5;
        a += 3; // 8
        a -= 2; // 6
        a *= 4; // 24
        a /= 3; //8
        a %= 5; //3
        System.out.println("a = " + a);
    }
}
~~~