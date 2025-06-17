---
layout: page
permalink: /blog/
---
<ul>
    <div class="posts">
      {% for post in site.posts %}
        {% if post.path contains 'blog' %}
          <article class="post">
            <h2><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h2>
          </article>
        {% endif %}
      {% endfor %}
    </div>
</ul>