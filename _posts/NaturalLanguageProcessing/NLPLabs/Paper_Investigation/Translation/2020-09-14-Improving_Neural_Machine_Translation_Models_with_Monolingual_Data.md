---
layout: post
title: Improving Neural Machine Translation Models with Monolingual Data. Sennrich et al. ACL. 2016.
subtitle: Title of paper - Improving Neural Machine Translation Models with Monolingual Data. Sennrich et al. ACL 2016.
category: NLP papers - Translation
tags: [translation]
permalink: /2020/09/14/Improving_Neural_Machine_Translation_Models_with_Monolingual_Data/
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

This is a brief summary of paper for me to study and organize it, [Improving Neural Machine Translation Models with Monolingual Data. Sennrich et al. ACL 2016](https://www.aclweb.org/anthology/P16-1009/) that I read and studied. 
{% include MathJax.html %}

This paper propose new data augmentation they call back-tranlsation. 

They focused that NMT has obtained state-of-the art performance for several language pair and that target-side monolingual data plays an important role in boosting fluency for phrased-based statistical mahicne translation.

So, they investigated the use of monolingual data for NMT. 

They experiemt two different methods to fill source side of monolingual training instance. 

One is to use **a dummy source sentence**, i.e. They pair monlingual setenences on target side with a single-word dummy source side **<null>** to allow processing of both parallel and monolingual trainig examples with the same network graph.

The other is to use a source sentence obtained via **back-translation**, which they call synthetic source sentence taht is obtained from automatically translating the target sentence into the source language.

They find that the latter is more effecitve. 

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Neural Machine Translation (NMT) has obtained state-of-the art performance for several language pairs, while only using parallel data for training. Targetside monolingual data plays an important role in boosting fluency for phrasebased statistical machine translation, and they investigate the use of monolingual data for NMT. In contrast to previous work, which combines NMT models with separately trained language models, they note that encoder-decoder NMT architectures already have the capacity to learn the same information as a language model, and they explore strategies to train with monolingual data without changing the neural network architecture. By pairing monolingual training data with an automatic backtranslation, they can treat it as additional parallel training data, and they obtain substantial improvements on the WMT 15 task English↔German (+2.8–3.7 BLEU), and for the low-resourced IWSLT 14 task Turkish→English (+2.1–3.4 BLEU), obtaining new state-of-the-art results. They also show that fine-tuning on in-domain monolingual and parallel data gives substantial improvements for the IWSLT 15 task English→German.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/P16-1009/">The paper: Improving Neural Machine Translation Models with Monolingual Data. Sennrich et al. ACL 2016</a>
</div>

# Reference 

- Paper 
  - [Arxiv version: Improving Neural Machine Translation Models with Monolingual Data. Sennrich et al. arXiv 2016](https://arxiv.org/abs/1511.06709)
  - [ACL 2016 version: Improving Neural Machine Translation Models with Monolingual Data. Sennrich et al. ACL 2016](https://www.aclweb.org/anthology/P16-1009/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    


