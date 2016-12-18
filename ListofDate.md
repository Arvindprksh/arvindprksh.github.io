---
layout: page
title: Things that,so far, I have been studying by date(Month and Year) 
subtitle: Something that I have studied and experienced, making List with what I have been studying
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---
{: #top }

[By Category]({{"/blog/archive/categoryview" | prepend: site.baseurl}}) | [By Tag Cloud]({{"/blog/archive/tagcloudview" | prepend: site.baseurl}}) | [All]({{ "/blog/archive/" | prepend: site.baseurl}})

<div id="posts-list">
{% assign openList = '<ul class="side-nav">' %}
{% assign closeList = '</ul>' %}
{% for post in site.posts %}
    {% capture month %}{{ post.date | date: '%m%Y' }}{% endcapture %}
    {% capture nmonth %}{{ post.next.date | date: '%m%Y' }}{% endcapture %}
    {% capture monthHead %}
        {% if month != nmonth %}
        {% if  forloop.index != 1  %}{{ closeList }}<small markdown="1"><!--[back to top](#top)--><a href="" class="btn btn-default">
      <span class="fa fa-refresh"></span> Go back to the top
    </a>  
    </small><hr/>{%endif %}
        <div class="post-preview"> 
        <h2 class="post-title">{% if year != nyear %}<a name="{{ post.date | date: '%Y' }}"></a>{% endif %}<a name="{{ post.date | date:  '%Y-%m'  }}"></a>{{ post.date | date: '%B %Y' }}</h2>
        {{ openList }}
        {% endif %}
    {% endcapture %}

    {% capture link %}
        <li>
            <a href="{{ site.baseurl }}{{ post.url }}"><strong>{{ post.title }}</strong><small class="post-meta"> - Posted on {{ post.date | date: "%B %-d, %Y" }}</small></a></li>
    {% endcapture %}
    
    {{ monthHead }}{{ link }}
{% endfor %}
{{closeList}}
        </div>
</div>
