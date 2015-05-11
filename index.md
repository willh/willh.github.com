---
layout: page
title: Will's Blog
tagline: 
---
{% include JB/setup %}

<div class="posts">
    {% for post in site.posts %}
        <div class="summary">
            <h3><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></h3>
            <p class="date">{{ post.date | date_to_string }}</p>
            <p>{{ post.description }}</p>
        </div>
    {% endfor %}
</div>
