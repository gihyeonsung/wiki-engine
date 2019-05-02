# 수정사항

+ 대문 게시글 카테고리로 구분해서 출력하도록 변경
```ruby
<h1>Blog Posts</h1>
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
```

```ruby
<h1>대문</h1>
<ul class="posts">
  {% for category in site.categories %}
    <h3>{{ category[0] }}</h3>
    <ul>
      {% for post in category[1] %}
        <li><span>{{ post.date | date_to_string }}</span> - <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
      {% endfor %}
    </ul>
  {% endfor %}
</ul>
```

+ HTML `theme-color`에서 `#B784D9`로 변경
+ CSS `.page-header background-color`에서 단색 `#5A2073`으로 변경
+ CSS `.main-content h1 .. h6`에서 `#B784D9`로 변경
+ CSS `.main-content code, pre, pre > code`에서 `#DAB6F2`로 변경