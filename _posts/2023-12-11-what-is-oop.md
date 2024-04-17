---
layout: post
title: Java - 객체 지향 프로그래밍(OOP)은 무엇인가?
subtitle: 김영한님의 Java 강의로 기초다지기 - 객체 지향 프로그래밍이란?
date: 2023-12-11
author: Warner
header-img: img/bg/post-bg-oop.jpg
catalog: true
tags:
  - Java
---

## 절차 지향 프로그래밍 vs 객체 지향 프로그래밍

프로그래밍 방식은 크게 절차 지향 프로그래밍과 객체 지향 프로그래밍으로 나눌 수 있다.

**절차 지향 프로그래밍**

- 절차 지향 프로그래밍은 이름 그대로 절차를 지향한다. 쉽게 이야기해서 실행 순서를 중요하게 생각하는 방식이다.
- 절차 지향 프로그래밍은 프로그램의 흐름을 순차적으로 따르며 처리하는 방식이다. 즉, "어떻게"를 중심으로 프로그래밍 한다.

**객체 지향 프로그래밍**

- 객체 지향 프로그래밍은 이름 그대로 객체를 지향한다. 쉽게 이야기해서 객체를 중요하게 생각하는 방식이다.
- 객체 지향 프로그래밍은 실제 세계의 사물이나 사건을 객체로 보고, 이러한 객체들 간의 상호작용을 중심으로 프로그래밍하는 방식이다. 즉, "무엇을" 중심으로 프로그래밍 한다.

**둘의 중요한 차이**

- 절차 지향은 데이터와 해당 데이터에 대한 처리 방식이 분리되어 있다. 반면 객체 지향에서는 데이터와 그 데이터에 대한 행동(메서드)이 하나의 '객체' 안에 포함되어 있다.

## 절차 지향 프로그래밍의 한계

~~~java
public class MusicPlayerMain2 {
    public static void main(String[] args) {
        MusicPlayerData data = new MusicPlayerData();
        on(data);
        volumeUp(data);
        volumeUp(data);
        volumeDown(data);
        showStatus(data);
        off(data);
    }

    private static void showStatus(MusicPlayerData data) {
        //음악 플레이어 상태
        System.out.println("음악 플레이어 상태 확인");
        if (data.isOn) {
            System.out.println("음악 플레이어 ON, 볼륨" + data.volume);
        } else {
            System.out.println("음악 플레이어 OFF");
        }
    }

    private static void on(MusicPlayerData data) {
        //음악 플레이어 켜기
        data.isOn = true;
        System.out.println("음악 플레이어를 시작합니다.");
    }

    private static void off(MusicPlayerData data) {
        //음악 플레이어 끄기
        data.isOn = false;
        System.out.println("음악 플레이어를 종료합니다.");
    }

    private static void volumeUp(MusicPlayerData data) {
        //볼륨 증가
        data.volume++;
        System.out.println("음악 플레이어 볼륨:" + data.volume);
    }

    private static void volumeDown(MusicPlayerData data) {
        //볼륨 감소
        data.volume--;
        System.out.println("음악 플레이어 볼륨:" + data.volume);
    }
}
~~~

> **모듈화** : 쉽게 이야기해서 레고 블럭을 생각하면 된다. 필요한 블럭을 가져다 꼽아서 사용할 수 있다.
> 여기서는 음악 플레이어의 기능이 필요하면 해당 기능을 메서드 호출 만으로 손쉽게 사용할 수 있다.

우리가 작성한 코드의 한계는 바로 데이터와 기능이 분리되어 있다는 점이다. 음악 플레이어의 데이터는 MusicPlayerData에 있는데, 그 데이터를 사용하는 기능은 MusicPlayerMain3에 있는 각각의
메서드에 분리되어 있다. 그래서 음악 플레이어와 관련된 데이터는 MusicPlayerData를 사용해야 하고, 음악 플레이어와 관련된 기능은 MusicPlayerMain3의 각 메서드를 사용해야 한다.

객체 지향 프로그래밍이 나오기 전까지는 지금과 같이 데이터와 기능이 분리되어 있었다. 따라서 지금과 같은 코드가 최선이었다. 하지만 객체 지향 프로그래밍이 나오면서 데이터와 기능을 온전히 하나로 묶어서 사용할 수
있게 되었다.

## 클래스와 메서드

클래스는 데이터인 멤버 변수 뿐 아니라 기능 역할을 하는 메서드도 포함할 수 있다.

~~~java
public class ValueData {
    int value;

    void add() {
        value++;
        System.out.println("숫자 증가 value = " + value);
    }
}
~~~

~~~java
public class ValueObjectMain {
    public static void main(String[] args) {
        ValueData valueData = new ValueData();
        valueData.add();
        valueData.add();
        valueData.add();
        System.out.println("valueData = " + valueData.value);
    }
}
~~~

**인스턴스 생성**
![object1.png](/img/post/2023/2023-12-11/object1.png)

**인스턴스의 메서드 호출**
![object2.png](/img/post/2023/2023-12-11/object2.png)

- 클래스는 속성(데이터, 멤버 변수)과 기능(메서드)을 정의할 수 있다.
- 객체는 자신의 메서드를 통해 자신의 멤버 변수에 접근할 수 있다.
    - 객체의 메서드 내부에서 접근하는 멤버 변수는 객체 자신의 멤버 변수이다.

## 객체 지향 프로그래밍

- 프로그램의 실행 순서 보다는 객체 만드는 것 자체에 집중해야 한다.
- 객체가 어떤 속성(데이터)을 가지고 어떤 기능(메서드)을 제공하는지 부분에 초점을 맞추어야 한다.

> **캡슐화**
> 객체의 속성과 기능이 하나로 묶어서 필요한 기능을 메서드를 통해 외부에 제공하는 것을 캡슐화라 한다.

## 객체란?
세상의 모든 사물을 단순하게 추상화해보면 속성(데이터)과 기능 딱 2가지로 설명할 수 있다.

**자동차**
- 속성 : 차량 생상, 현재 속도
- 기능 : 엑셀, 브레이크, 문 열기, 문 닫기

**동물**
- 속성 : 색상, 키, 온도
- 기능 : 먹는다. 걷는다.

**게임 캐릭터**
- 속성 : 레벨, 경험치, 소유한 아이템들
- 기능 : 이동, 공격, 아이템 획득

객체 지향 프로그래밍은 모든 사물을 속성과 기능을 가진 객체로 생각하는 것이다.\
객체에는 속성과 기능만 존재한다.\
이렇게 단순화하면 세상에 있는 객체들을 컴퓨터 프로그램으로 쉽게 설계할 수 있다.\
이런 장점들 덕분에 지금은 객체 지향 프로그래밍이 가장 많이 사용된다.\
참고로 실세계와 객체가 항상 1:1로 매칭되는 것은 아니다.
