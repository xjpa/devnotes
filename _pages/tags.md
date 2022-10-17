---
layout: page
title: 'Tags/Categories'
---

<div class="tags-expo">
  <div class="tags-expo-list">
  
  <ul>
    {% for tag in site.tags %}
    <li><a href="#{{ tag[0] | slugify }}" class="post-tag">{{ tag[0] }}</a> ({{tag[1].size}})</li>
    {% endfor %}
    </ul>
  </div>

<br><hr/><br>

  <div class="tags-expo-section">
    {% for tag in site.tags %}
    <h2 id="{{ tag[0] | slugify }}">{{ tag | first }}</h2>
    <ul class="tags-expo-posts">
      {% for post in tag[1] %}
      <li>
{{ post.date | date:"%Y-%m-%d" }}
<a class="post-title" href="{{ site.baseurl }}{{ post.url }}">
        {{ post.title }}      </a>
      </li>
      {% endfor %}
    </ul>
    {% endfor %}
  </div>
</div>
