---
layout: page
permalink: /photos/
---

<ul>
    <div class="posts">
      {% for post in site.posts %}
        {% if post.path contains 'photos' %}
          <article class="photos">
            <h2><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h2>
          </article>
        {% endif %}
      {% endfor %}
    </div>
</ul>