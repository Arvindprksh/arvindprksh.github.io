---
layout: page
title: "Blog Archive by Category"
---

[By Date]({{"/blog/archive/monthview" | prepend: site.baseurl}}) | [By Tag Cloud]({{"/blog/archive/tagcloudview" | prepend: site.baseurl}}) | [All]({{ "/blog/archive/" | prepend: site.baseurl}})

{% assign tags = site.categories | sort %}
{% assign sorted_posts = site.posts | sort: 'title' %}

{% assign tags_url = '' %}
{% include _tag_cloud.html baseurl=tags_url %}


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

