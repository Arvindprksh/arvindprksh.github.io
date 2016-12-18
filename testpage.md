---
layout: page
title: "Blog Archive by Category"
---


{% assign tags = site.categories | sort %}
{% assign sorted_posts = site.posts | sort: 'title' %}

{% assign tags_url = '' %}

{% assign tags = site.categories | sort %}
{% assign baseurl = include.baseurl %}
{% assign increaseFont = include.tagCloud %}

<div id="category-index" class="row">
	<div class="small-12 columns t30">
        <div class="tagcloud03">
            <ul{% if increaseFont %} class="cloud"{% endif %}> {% for tag in tags %}<li><a href="{{baseurl}}#{{ tag | first | slugify }}" {% if increaseFont %}style="font-size: {{ tag | last | size  |  times: 4 | plus: 80  }}%"{% endif %}>{{ tag | first | replace: '-', ' ' }}{% unless increaseFont %}<span>{{ tag | last | size }}</span>{% endunless %}</a></li>{% endfor %}
            </ul>
        </div><!-- /.tagcloud03 -->
    </div><!-- /.small-12.columns -->
</div><!-- /.row -->

<div id="blog-index" class="row columns">
{% for tag in tags %}

<h3 class="archivetitle"><a name="{{ tag | first | slugify }}"></a>{{ tag | first | replace:'-', ' ' }} <i class="badge">{{ tag | last | size }}</i> </h3>

<ul class="side-nav">

{% for post in sorted_posts %}
    {%if post.categories contains tag[0]%}
<li>
    <a title="Read {{ post.title | escape_once }}"   href="{{ site.baseurl }}{{ post.url }}"> <strong>{{ post.title }}</strong>{% if post.date %}<small> - {{ post.date | date: "%B %e, %Y" }}</small>{% endif %}</a>
 </li>
    {%endif%}

{% endfor %}
</ul>

<small markdown="1"></small>

{% endfor %}
</div>

