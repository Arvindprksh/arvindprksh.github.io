---
layout: post
title: Transfer Learning for Low-Resource Neural Machine Translation. Zoph et al. EMNLP. 2016.
subtitle: Title of paper - Transfer Learning for Low-Resource Neural Machine Translation. Zoph et al. EMNLP. 2016.
category: NLP papers - Translation
tags: [transfer learning, translation]
permalink: /2020/06/17/Transfer_Learning_for_Low-Resource_Neural_Machine_Translation/
css : /css/ForYouTubeByHyun.css
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
  
---

This is a brief summary of paper for me to note it, [Transfer Learning for Low-Resource Neural Machine Translation. Zoph et al. EMNLP 2016](https://www.aclweb.org/anthology/D16-1163/)

{% include MathJax.html %}

This paper experiment a variety of scenarios for low-resource langauge with transfer learning.

They trained the sequence-to-sequence model for high-resource langauge pair as parent model. 

Next, transfer some of the learned parameters to the low-resource lanauge pair as child model to initialize and constrain training. 

In other words, **their key idea is to first train a high-resource language pair (the parent model), then transfer some of the
learned parameters to the low-resource pair (the child model) to initialize and constrain training**.

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
The encoder-decoder framework for neural machine translation (NMT) has been shown effective in large data scenarios, but is much less effective for low-resource languages. They present a transfer learning method that significantly improves BLEU scores across a range of low-resource languages. They key idea is to first train a high-resource language pair (the parent model), then transfer some of the learned parameters to the low-resource pair (the child model) to initialize and constrain training. 
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/D16-1163/">The paper: Transfer Learning for Low-Resource Neural Machine Translation. Zoph et al. EMNLP 2016</a>
</div>

# Reference 

- Paper 
  - [ArXiv version: Transfer Learning for Low-Resource Neural Machine Translation. Zoph et al. ArXiv 2016](https://arxiv.org/abs/1604.02201)
  - [EMNLP version: Transfer Learning for Low-Resource Neural Machine Translation. Zoph et al. EMNLP 2016](https://www.aclweb.org/anthology/D16-1163/)
  
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
