---
layout: post
title: Github Blog-3 검색창 노출시키기
subtitle: sitemap.xml, google search console, naver search advisor 사용
date: 2023-11-09
author: Warner
header-img: img/bg/post-bg-keybord.jpg
catalog: true
tags:
  - Github 
---

## 1. sitemap.xml 만들기

![sitemap code.png](/img/post/2023-11-09/sitemap-code.png)
**주의! 사이트맵 코드 들여쓰기 한번더 확인하기**

## 2. robots.txt만들기

~~~markdown
User-agent: *
Allow: /

Sitemap: https://eona1301.github.io/sitemap.xml
~~~

## 3. Google search Cosole 등록

![google1.png](/img/post/2023-11-09/google1.png)
**github pages url을 사용함으로 url로 등록**

![google2.png](/img/post/2023-11-09/google2.png)
**만든 sitemap.xml 등록**

## 4. Naver Search Advisor

![naver-search1.png](/img/post/2023-11-09/naver-search1.png)
**github blog url 입력**

![naver-search2.png](/img/post/2023-11-09/naver-search2.png)
**만든 sitemap.xml 등록**