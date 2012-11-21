---
layout: page
title : Erlang
header : Post Archive
group: navigation
---
<!-- {% include JB/setup %} -->

<!-- {% assign posts_collate = site.posts.erlang %}
{% include JB/posts_collate %} -->

<ul>
  {% for post in site.posts %}
    <li>
    	<span>{{ post.date | date_to_string }}</span> &raquo; 
    	<a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
##Erlang Pages

	-module(erlang).
	-export([e/0]).
	e()->
		io:format("hello world").