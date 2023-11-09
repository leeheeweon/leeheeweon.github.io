---
layout:     post
title:      Github Blog 검색창 노출시키기
subtitle:   sitemap.xml, google search console, naver search advisor 사용 
date:       2023-11-09
author:     Warner
header-img: img/post-bg-keybord.jpg
catalog: true
tags:
    - Github 
---

## 1. sitemap.xml 만들기
~~~text
---
layout: null
---

<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9 http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd"
        xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
    {% for post in site.posts %}
    <url>
        <loc>{{ site.url }}{{ post.url }}</loc>
        {% if post.lastmod == null %}
        <lastmod>{{ post.date | date_to_xmlschema }}</lastmod>
        {% else %}
        <lastmod>{{ post.lastmod | date_to_xmlschema }}</lastmod>
        {% endif %}

        {% if post.sitemap.changefreq == null %}
        <changefreq>weekly</changefreq>
        {% else %}
        <changefreq>{{ post.sitemap.changefreq }}</changefreq>
        {% endif %}

        {% if post.sitemap.priority == null %}
        <priority>0.5</priority>
        {% else %}
        <priority>{{ post.sitemap.priority }}</priority>
        {% endif %}

    </url>
    {% endfor %}
</urlset>
~~~
**주의! 사이트맵 코드 들여쓰기 한번더 확인하기**

## 2. robots.txt만들기
~~~text
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