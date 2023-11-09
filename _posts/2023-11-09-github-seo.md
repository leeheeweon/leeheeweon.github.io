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

<pre class=" language-xml"><code class=" language-xml">---
layout: null
---

<span class="token prolog">&lt;?xml version="1.0" encoding="UTF-8"?&gt;</span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>urlset</span> <span class="token attr-name"><span class="token namespace">xmlns:</span>xsi</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>http://www.w3.org/2001/XMLSchema-instance<span class="token punctuation">"</span></span>
        <span class="token attr-name"><span class="token namespace">xsi:</span>schemaLocation</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>http://www.sitemaps.org/schemas/sitemap/0.9 http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd<span class="token punctuation">"</span></span>
        <span class="token attr-name">xmlns</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>http://www.sitemaps.org/schemas/sitemap/0.9<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
    {% for post in site.posts %}
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>url</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>loc</span><span class="token punctuation">&gt;</span></span>{{ site.url }}{{ post.url }}<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>loc</span><span class="token punctuation">&gt;</span></span>
        {% if post.lastmod == null %}
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>lastmod</span><span class="token punctuation">&gt;</span></span>{{ post.date | date_to_xmlschema }}<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>lastmod</span><span class="token punctuation">&gt;</span></span>
        {% else %}
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>lastmod</span><span class="token punctuation">&gt;</span></span>{{ post.lastmod | date_to_xmlschema }}<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>lastmod</span><span class="token punctuation">&gt;</span></span>
        {% endif %}

        {% if post.sitemap.changefreq == null %}
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>changefreq</span><span class="token punctuation">&gt;</span></span>weekly<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>changefreq</span><span class="token punctuation">&gt;</span></span>
        {% else %}
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>changefreq</span><span class="token punctuation">&gt;</span></span>{{ post.sitemap.changefreq }}<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>changefreq</span><span class="token punctuation">&gt;</span></span>
        {% endif %}

        {% if post.sitemap.priority == null %}
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>priority</span><span class="token punctuation">&gt;</span></span>0.5<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>priority</span><span class="token punctuation">&gt;</span></span>
        {% else %}
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>priority</span><span class="token punctuation">&gt;</span></span>{{ post.sitemap.priority }}<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>priority</span><span class="token punctuation">&gt;</span></span>
        {% endif %}

    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>url</span><span class="token punctuation">&gt;</span></span>
    {% endfor %}
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>urlset</span><span class="token punctuation">&gt;</span></span></code></pre>

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