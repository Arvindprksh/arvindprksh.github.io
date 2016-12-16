---
layout: page
title: "by Tag Cloud2"
---
<!--
{% assign tags = site.tags | sort %}
{% for tag in tags %}
 <span class="site-tag">
    <a href="/tag/{{ tag | first | slugize }}/"
        style="font-size: {{ tag | last | size  |  times: 4 | divided_by: site.tags.size | plus: 80  }}%">
            {{ tag[0] | replace:'-', ' ' }} {{ tag | last | size }}
    </a>
</span>
{% endfor %}
-->

{% assign tags = site.tags | sort %}
{% for tag in site.tags %}
    <li style="font-size: {{ tag | last | size | times: 100 | divided_by: site.tags.size }}%">
        <a href="/{{ tag | first | slugize }}/">
            {{ tag | first }}
        </a>
    </li>
{% endfor %}
