---
layout: page
permalink: /photos/
---

<div class="gallery">
  {% for file in site.static_files %}
    {% if file.path contains 'images/photos' %}
        <img src="/img/blank.png" alt="" data-echo="{{ file.path }}">
    {% endif %}
 {% endfor %}
</div>