---
layout: post
title: Java - What is Primitive type and reference type? (기본형과 참조형이란?)
subtitle: 김영한님의 Java 강의로 기초다지기 - 기본형과 참조형이란?
date: 2023-12-09
author: Warner
header-img: img/bg/post-bg-point.jpg
catalog: true
tags:
  - Java
---

## 시작

변수의 데이터 타입을 가장 크게 보면 기본형과 참조형으로 분류할 수 있다.

- **기본형(Primitive Type)**: int, long, double, boolean 사용하는 값을 변수에 직접넣을 수 있다.
- **참조형(Reference Type)**: Student student1, int[] students 객체가 저장된 메모리의 위치를 가르키는 참조값을 넣을 수 있다.

## 기본

- 기본형은 숫자 10, 20과 같이 실제 사용하는 값을 변수에 담을 수 있다.
- 참조형은 실제 사용하는 값을 변수에 담는 것이 아니다. 이름 그대로 실제 객체의 위치(참조, 주소)를 저장한다. 참조형에는 객체와 배열이 있다.
    - 객체는 .(dot)을 통해서 메모리 상에 생성된 객체를 찾아가야 사용할 수 있다.
    - 배열은 [] 를 통해서 메모리 상에 생성된 배열을 찾아가야 사용할 수 있다.

## 계산

기본형 연산가능

~~~java
int a=10,b=20;
int sum=a+b;
~~~

참조형은 계산에 사용할 수 없다.

~~~java
Student s1=new Student();
Student s2=new Student();
s1+s2 //오류 발생
~~~

**참고 - String**
자바에서 String은 특별하다. String은 사실은 클래스다. 따라서 참조형이다. 그런데 기본형처럼 문자 값을 바로 대입할 수 있다.
문자는 매우 자주 다루기 때문에 자바에서 특별하게 편의 기능을 제공한다. String에 대한 자세한 내용은 뒤에서 설명한다.

## 변수 대입

**대원칙 : 자바는 항상 변수의 값을 복사해서 대입한다.**

기본형 대입

~~~java
int a=10;
int b=a;
~~~

참조형 대입

~~~java
Student s1=new Student();
Student s2=s1;
~~~

**참조형의 경우 실제 사용하는 객체가 아니라 객체의 위치를 가르키는 참조값만 복사된다.**

## null

택배를 보낼 때 제품은 준비가 되었지만, 보낼 주소지가 아직 결정되지 않아서, 주소지가 결정될 때 까지는 주소지를 비워두어야 할 수 있다.

참조형 변수에는 항상 객체가 있는 위치를 가리키는 참조값이 들어간다. 그런데 아직 가리키는 대상이 없거나, 가리키는 대상을 나중에 입력하고 싶다면 어떻게 해야할까?

참조형 변수에는 아직 가리키는 대상이 없다면 null 이라는 특별한 값을 넣어둘 수 있다. null은 값이 존재하지 않는, 없다는 뜻이다.

**Data data = null**
![null1.png](/img/post/2023-12-09/null1.png)

Data 타입을 받을 수 있는 참조형 변수 data를 만들었다. 그리고 여기에 null 값을 할당했다. 따라서 data 변수에는 아직 가리키는 객체가 없다는 뜻이다.

**data = new Data()**
![null2.png](/img/post/2023-12-09/null2.png)

이후에 새로운 Data 객체를 생성해서 그 참조값을 data 변수에 할당했다. 이제 data 변수가 참조할 객체가 존재한다.

**data = null**
![null3.png](/img/post/2023-12-09/null3.png)
마지막에는 data에 다시 null값을 할당했다. 이렇게 하면 data 변수는 앞서 만든 Data 인스턴스를 더는 참조하지 않는다.

**GC - 아무도 참조하지 않는 인스턴스의 최후**
![null4.png](/img/post/2023-12-09/null4.png)

아무도 참조하지 않는 인스턴스는 사용되지 않고 메모리 용량만 차지할 뿐이다.\
자바는 이런 과정을 자동으로 처리해준다. 아무도 참조하지 않는 인스턴스가 있으면 JVM의 GC(가비지 컬렉션)가 더 이상 사용하지 않는 인스턴스라 판단하고 해당 인스턴스를 자동으로 메모리에서 제거해준다.

## NullPointerException
택배를 보낼 때 주소지 없이 택배를 발송하면 어떤 문제가 발생할까? 만약 참조값 없이 객체를 찾아가면 어떤 문제가 발생할까?

이 경우 NullPointerException 이라는 예외가 발생하는데, 개발자를 가장 많이 괴롭히는 예외이다.\
NullPointerException은 이름 그대로 null을 가리키다(Pointer)인데, 이때 발샣하는 예외(Exception)다.\
null은 없다는 뜻이므로 결국 주소가 없는 곳을 찾아갈 때 발생하는 예외이다.

