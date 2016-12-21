---
layout: page
title: Study List With Categories
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

Before going to Silicon Valley, I love challenge to new technology, I made git static page to arrange concept of computer sceince for myself. I started studying the Data structure, algorithm and OS(operating system). that is a good time to remember knowledge I forgot. And, continuously while I'm doing OpenSource project In Silicon Valley,CA, I will make a note about what I learn. 

요즘 미국 실리콘 밸리로 인턴을 떠나기 전에 심심해서 지금의 Git-Hub을 이용해 내 홈페이지를 만들고, 자바 "자바의 정석", 열혈강의 C/C++, 자료구조, os(운영체제) 등을 다시 학습을 하기 시작했다. 이를 통해 그동안 잊고 지냈던 개념들을 다시 알게 되어 좋은 시간인거 같다. 또한 미국에서 리눅스 관련 OpenSource 작업을 하면서 필요한 정보들을 그때 그때 정리해놓아서 나중에 많은 도움을 받을 수 있을 거 같다.

{: #top }

<!-- this code si from https://github.com/daattali/daattali.github.io/blob/master/index.html --> 
<div class="list-filters post-preview">
  <a href="/" class="list-filter">All posts</a>
  <a href="/alistofcategories" class="list-filter filter-selected">Catergories Cloud</a>
  <a href="/alistofcloudoftags" class="list-filter">Tags Cloud</a>
  <a href="/alistofdate" class="list-filter">Date Cloud</a>
</div>


<!-- I follow the file from cloudoftags file of my github(https://github.com/hyunyoung2/hyunyoung2.github.io/blob/master/cloudoftags.html)-->

<!-- this code from https://github.com/codinfox/codinfox-lanyon/blob/dev/blog/categories.html-->
<div class="posts-list">
  <div class="blog-tags"> 
    {% assign tags = site.tags | sort %}
    {% for tag in tags %}
    <a href="#{{ tag[0] | slugify }}" class="btn btn-default" style="font-size: {{ tag | last | size  |  times: 4 | plus: 80  }}%"> <!-- style="color: #1C1C1C;" -->
      <span class="fa fa-folder-open" aria-hidden="true" style="color: #1C1C1C;"> <!-- I get rid of left option -->
        {{ tag[0] }} <i class="badge">{{ tag | last | size }}</i>
      </span>
    </a>
    {% endfor %}
  </div>
  <hr/> <!-- margin-top and margin-bottom in main.css -->
  <div class="post-preview"> <!--post-preview -->
    {% for tag in tags %} <!-- style="padding-top: 70px;" is used to deal with nav-custom bar -->
      <h2 id="{{ tag[0] | slugify }}" style="padding-top: 70px;"> {{ tag[0] }}  <i class="badge">{{ tag | last | size }}</i></h2> <!-- I added new class -->
      <ul class="later on"> <!-- post-subtitle -->
        {% for post in tag[1] %}
          <a class="post-subtitle" href="{{ site.baseurl }}{{ post.url }}">
        <li>
          {{ post.title }}
        <small class="post-meta"> - Posted on {{ post.date | date: "%B %-d, %Y" }}</small>
        </li>
        </a>
        {% endfor %}
      </ul>
        <a href="#top" class="btn btn-default" style="font-size: 15px; padding: 0px 10px; margin-left: 30px">
          <span class="fa fa-refresh" aria-hidden="true" style="margin-left: 30px"></span> Go back to the top
        </a> 
        <hr/>
    {% endfor %}
  </div>
</div>
