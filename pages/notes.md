---
layout: page
permalink: /blog/
---
<ul>
    <div class="posts">
      {% for post in site.posts %}
        {% if post.path contains 'blog' %}
          <article class="post">
            <li>
            <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
            <p class="date">{{ post.date | date: "%B %e, %Y" }}</p>
            </li>
          </article>
        {% endif %}
      {% endfor %}
    </div>
</ul>
