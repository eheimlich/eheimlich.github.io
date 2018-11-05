---
layout: archive
permalink: /resume/
author_profile : true
---
Download Resume: [Ethan's Resume](/documents/Ethan_Heimlich_Resume.pdf)
![Resume](/images/resume.jpg)


{% for tag in group_names %}
  {% assign posts = group_items[forloop.index0] %}
  <h2 id="{{ tag | slugify }}" class="archive__subtitle">{{ tag }}</h2>
  {% for post in posts %}
    {% include archive-single.html %}
  {% endfor %}
{% endfor %}
