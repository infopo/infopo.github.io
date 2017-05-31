---
layout: page
title: Category
permalink: /category/
sitemap: false
---

<!-- 전체 카테고리를 수평으로 나열 -->
<div>
{% assign categories = site.categories | sort %}

{% for category in categories %}
  <span class="site-tag">
    <a href="#{{ category | first | slugify }}">
      {{ category[0] | replace:'-', ' ' }} ({{ category | last | size }}) &nbsp;&nbsp;
    </a>
  </span>
{% endfor %}
</div>

<!-- 각 카테고리와 그에 해당하는 내용 출력 -->
<div id="index">
{% for category in categories %}
 <a name="{{ category[0] }}"></a>
 <h2>{{ category[0] | replace:'-', ' ' }} ({{ category | last | size }})</h2>
 <!--{% assign sorted_posts = site.posts | sort: 'title' %}--> <!--이건 제목별로 정렬(원본)-->
 {% assign sorted_posts = site.posts | sort: 'date' | sort: 'title' %} <!--날짜, 제목 이중정렬 -->
   {% for post in sorted_posts %}
    {%if post.categories contains category[0]%}
      <a class="post-title" href="{{ site.baseurl }}{{ post.url }}">
        <li>
          {{ post.title }}
          <small class="post-date">{{ post.date |  date_to_string }}</small>
        </li>
      </a>
    {%endif%}
   {% endfor %}
{% endfor %}
</div>
