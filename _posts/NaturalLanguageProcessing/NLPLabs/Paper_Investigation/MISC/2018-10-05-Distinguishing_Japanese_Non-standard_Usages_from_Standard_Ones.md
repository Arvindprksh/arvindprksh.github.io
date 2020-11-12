---
layout: post
title: Distinguishing Japanese Non-standard Usages from Standard Ones
subtitle: Title of paper - Distinguishing Japanese Non-standard Usages from Standard Ones
category: NLP papers - MISC
tags: [nlp, word2vec, emnlp]
permalink: /2018/10/05/Distinguishing_Japanese_Non-standard_Usages_from_Standard_Ones/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

This paper's title is [Distinguishing Japanese Non-standard Usages from Standard Ones. Aoki et al. EMNLP 2017](https://www.aclweb.org/anthology/D17-1246).

The following is what I prepared for for paper seminar of  NLP labs.

<iframe src="//www.slideshare.net/slideshow/embed_code/key/oKiTrIuvjAWn6V" width="595" height="485" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="//www.slideshare.net/HyunYoungLee3/distinguishing-japanese-non-standard-usage-from-standard-ones" title="Distinguishing japanese non standard usage from standard ones" target="_blank">Distinguishing japanese non standard usage from standard ones</a> </strong> from <strong><a href="https://www.slideshare.net/HyunYoungLee3" target="_blank">hyunyoung Lee</a></strong> </div>


I think this paper is interesting to use out-embedding, in here they used out-embedding predicting context word on Skip-gram method.

<div class="alert alert-success" role="alert"><i class="fa fa-check-square-o"></i> <b>Tip: </b>
word embedding, in-embedding, out-embedding, distance weight(decay weight)
</div>


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note: </b>
This paper focus on non-standard usages of common words on social media. In the context of social media. words sometimes have other usages that ar totally different from their original. so this paper attempt to distinguish non-standard usages on social meadia from standard ones in an unsupervised manner. The their idea is based on mesuaring consistency between the expected meaning of the target word and the given context. For this purpose, They used context embedding derived from word embedding on Skip gram
</div>
  
  
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/D17-1246">The paper: Distinguishing Japanese Non-standard Usages from Standard Ones</a>
</div>

# Reference 

- Paper 
  - [EMNLP Version: Distinguishing Japanese Non-standard Usages from Standard Ones. Aoki et al. EMNLP 2017](https://www.aclweb.org/anthology/D17-1246)
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html) 
