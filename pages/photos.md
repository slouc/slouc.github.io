---
layout: page
permalink: /places/
---
<ul>
    <div class="posts">
      {% for post in site.posts %}
        {% if post.path contains 'places' %}
          <article class="places">
            <li><h2><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h2></li>
          </article>
        {% endif %}
      {% endfor %}
    </div>
</ul>