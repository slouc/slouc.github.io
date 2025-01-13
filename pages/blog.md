---
layout: page
permalink: /blog/
---
<ul>
    <div class="posts">
      {% for post in site.posts %}
        <article class="post">
          <li><h1><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h1></li>
        </article>
    {% endfor %}
    </div>
</ul>