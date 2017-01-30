---
layout: page
title: Study List With Date
subtitle: Something that I have studied and experienced
css: "/css/cloudlistfilter.css"
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

Before going to Silicon Valley, I love challenge to new technology, I made git static page to arrange concept of computer sceince for myself. I started studying the Data structure, algorithm and OS(operating system). that is a good time to remember knowledge I forgot. And, continuously while I'm doing OpenSource project In Silicon Valley, CA, I will make a note about what I learn. 

요즘 미국 실리콘 밸리로 인턴을 떠나기 전에 심심해서 지금의 Git-Hub을 이용해 내 홈페이지를 만들고, 자바 "자바의 정석", 열혈강의 C/C++, 자료구조, os(운영체제) 등을 다시 학습을 하기 시작했다. 이를 통해 그동안 잊고 지냈던 개념들을 다시 알게 되어 좋은 시간인거 같다. 또한 미국에서 리눅스 관련 OpenSource 작업을 하면서 필요한 정보들을 그때 그때 정리해놓아서 나중에 많은 도움을 받을 수 있을 거 같다.

{: #top }

<!-- this code si from https://github.com/daattali/daattali.github.io/blob/master/index.html --> 
<div class="list-filters post-preview">
  <a href="/" class="list-filter">All posts</a>
  <a href="/alistofcategories" class="list-filter">Catergories Cloud</a>
  <a href="/alistofcloudoftags" class="list-filter">Tags Cloud</a>
  <a href="/alistofdate" class="list-filter filter-selected">List by Date</a>
</div>

<!-- This code from another person of https://github.com/digitaldrummerj/digitaldrummerj.github.io/blob/master/blog/archivebydate-->

<div class="">
{% assign openList = '<ul class="later on">' %}
{% assign closeList = '</ul>' %}
<!-- for index of date, this code comes from https://github.com/digitaldrummerj/digitaldrummerj.github.io/blob/master/_includes/_sidebar.html-->

	{% assign archive_url = site.baseurl | append: '/alistofdate/' %}
	{% for post in site.posts %}
		{% assign currentdate = post.date | date: '%B %Y' %}
			{% if currentdate != date %}
				{% unless forloop.first %}
					<i class="badge">{{ count }}</i></span></a>
				{% endunless %}
				{% assign count = 1 %}
				{% assign currentyear = post.date | date: '%Y' %}
				{% if currentyear != year %}
					{% unless forloop.first %}
					<hr/>
					{% endunless %}
					<h3>
					<span class="fa fa-calendar" aria-hidden="true"></span>
					<a href="{{ archive_url }}#{{ currentyear }}">{{ currentyear }}</a>
					</h3>
					{% assign year = currentyear %}
				{% endif %}
				<a href="{{ archive_url }}#{{ currentdate }}"  class="btn btn-default" style="padding: 0px 5px;"><span class="fa fa-folder-open" aria-hidden="true" style="color: #1C1C1C;">{{ post.date | date: '%B' }} <!-- style="color: #1C1C1C;" is font color of span -->
				{% assign date = currentdate %}
			{% else %}
				{% assign count = count | plus: 1 %}
			{% endif %}
			{% if forloop.last %}
				<i class="badge">{{ count }}</i></span></a><hr/>
			{% endif %}
	{% endfor %}
	

{% for post in site.posts %}
    {% capture month %}
      {{ post.date | date: '%m%Y' }}
    {% endcapture %}

    {% capture nmonth %}
      {{ post.next.date | date: '%m%Y' }}
    {% endcapture %}

      {% capture monthHead %}
        {% if month != nmonth %}
          {% if  forloop.index != 1  %}
              {{ closeList }}
              <small markdown="1"><!--[back to top](#top)-->
                <a href="#top" class="btn btn-default" style="font-size: 15px; padding: 0px 5px; margin-left: 30px">
                  <span class="fa fa-refresh" aria-hidden="true"></span> Go back to the top
                </a>
              </small>
              
          {%endif %}
        <h2 class="" style="padding-top: 70px">
            {% if year != nyear %}
             <a name="{{ post.date | date: '%Y' }}"></a>
            {% endif %} 
          <a name="{{ post.date | date:  '%B %Y'  }}"></a>
          {{ post.date | date: '%B %Y' }}
       </h2>{{ openList }}
      {% endif %}
    {% endcapture %}

    {% capture link %}
        <li>
            <a class="post-subtitle" href="{{ site.baseurl }}{{ post.url }}">
              <strong>{{ post.title }}</strong>
              <small class="post-meta"> - Posted on {{ post.date | date: "%B %-d, %Y" }}</small>
            </a>
        </li>
    {% endcapture %}

    <div class="post-preview">{{ monthHead }}</div>{{ link }}
       
{% endfor %}
{{closeList}}
    <small markdown="1"><!--[back to top](#top)-->
       <a href="#top" class="btn btn-default" style="font-size: 15px; padding: 0px 5px; margin-left: 30px">
         <span class="fa fa-refresh" aria-hidden="true"></span> Go back to the top
       </a>
    </small>
    <hr/>
</div>

