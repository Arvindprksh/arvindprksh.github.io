---
layout: page
title: "Blog Archive by Date"
---
{: #top }

[By Category]({{"/blog/archive/categoryview" | prepend: site.baseurl}}) | [By Tag Cloud]({{"/blog/archive/tagcloudview" | prepend: site.baseurl}}) | [All]({{ "/blog/archive/" | prepend: site.baseurl}})

<div id="index">
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
    <hr/></small>{%endif %}
        <h2 class="archivetitle">{% if year != nyear %}<a name="{{ post.date | date: '%Y' }}"></a>{% endif %}<a name="{{ post.date | date:  '%Y-%m'  }}"></a>{{ post.date | date: '%B %Y' }}</h2>
        {{ openList }}
        {% endif %}
    {% endcapture %}

    {% capture link %}
        <li>
            <a title="Read {{ post.title | escape_once }}" href="{{ site.baseurl }}{{ post.url }}"><strong>{{ post.title }}</strong><small class="post-meta"> - Posted on {{ post.date | date: "%B %-d, %Y" }}</small></a></li>
    {% endcapture %}
    
    {{ monthHead }}{{ link }}
{% endfor %}
{{closeList}}
</div>
