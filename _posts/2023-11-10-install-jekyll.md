---
layout: post
title: GitHub Blog Jekyll 설치 및 GitHub Repository clone - 2
subtitle: Jekyll란,  GitHub Repository clone 
date: 2023-11-10
author: Warner
header-img: img/bg/home-bg-o.jpg
catalog: true
tags:
  - Github
---

## Jekyll 이란?
Ruby 로 만들어진 정적 사이트 생성기이다. 보통 지킬 이라고 읽는다.
참고로 Jekyll 을 설치하지 않아도 GitHub Blog 는 만들 수 있다.

## Jekyll 은 왜 설치할까?
웹 페이지를 수정하고 GitHub 에 Commit/Push 를 하면 GitHub Blog 에 반영이 된다.
따라서 GitHub Blog 의 페이지를 수정하고 이 수정된 내용을 확인하기 위해선,
GitHub 에 Push 후 해당 도메인에 들어가야만 확인이 가능하다.
그래서 수정한 내용을 웹 사이트에 올리기 전 Jekyll 을 깔아 의도한 대로 페이지가 작성됬는지 확인하는 작업이 필요하다.
즉 실제 웹 페이지에 올리기전에 **내 로컬 컴퓨터에서 확인**하기 위해 설치한다.

## Jekyll 설치
### Ruby 설치
Jekyll 은 Ruby의 패키지 매니저인 Gem 을 사용해서 설치할 수 있다.
그리고 이 Gem 을 사용하기 위해선 Ruby 를 우선 설치해야 한다.

Ruby 는 RubyInstaller 에서 다운 가능하다.
![ruby1.png](/img/post/2023-11-10/ruby1.png)

![ruby2.png](/img/post/2023-11-10/ruby2.png)

cmd 창에 아래 명령어로 jekyll 설치 및 버전 확인
~~~markdown
gem install jekyll bundler
jekyll -v
~~~

## 소스코드 편집기 다운로드 
[인텔리제이](https://www.jetbrains.com/ko-kr/idea/) 또는 [Visual Studio Code](https://code.visualstudio.com/) 추천


## Git 다운로드 
[Git](https://git-scm.com/)

## Repository 클론받기 
![clone1.png](/img/post/2023-11-10/clone1.png)


저장을 원하는 위치로 이동해서 마우스 우클릭 gitbash 를 열어준다.

git clone 복사된 ssh 입력
~~~git
 git clone git@github.com:leeheeweon/leeheeweon.github.io.git
~~~
![clone2.png](/img/post/2023-11-10/clone2.png)

3편에서 계속 