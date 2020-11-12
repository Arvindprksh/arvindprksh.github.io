---
layout: post
title: Learned in Translation - Contextualized Word Vectors
subtitle: Title of paper - Learned in Translation - Contextualized Word Vectors
category: NLP papers - Transfer Learning
tags: [neural network, contextual embedding, text classification]
permalink: /2019/11/19/Learned_in_Translation-Contextualized_Word_Vectors/
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

This is a brief summary of paper for me to study and organize it, [Learned in Translation: Contextualized Word Vectors (McCann et al. NIPS 2017)](http://papers.nips.cc/paper/7209-learned-in-translation-contextualized-word-vectors) I read and studied. 
{% include MathJax.html %}


They have a focus on transfer-learning from Machine translation task to downstream tasks of NLP. 


<div id="tutorial-section">

  <div id="tutorial-title">Learned in Translation: Contextualized Word Vectors</div>

  <ul class="nav nav-pills">
    <li class="active"><a data-toggle="tab" href="#refrigerator">NLP labs Seminar</a></li>
  </ul>

  <div class="tab-content">
    <div id="refrigerator" class="tab-pane fade in active">
      <iframe src="//www.slideshare.net/slideshow/embed_code/key/vvGRi1gjMZZ6vI" width="560" height="315" frameborder="0" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="//www.slideshare.net/HyunYoungLee3/paper-seminarlearned-in-translation-contextualized-word-vectors-216501634" title="(Paper seminar)Learned in Translation: Contextualized Word Vectors" target="_blank">(Paper seminar)Learned in Translation: Contextualized Word Vectors</a> </strong> from <strong><a href="https://www.slideshare.net/HyunYoungLee3" target="_blank">hyunyoung Lee</a></strong> </div>
    </div>
  </div>
</div>

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Computer vision has benefited from initializing multiple deep layers with weights pretrained on large supervised training sets like ImageNet. Natural language processing (NLP) typically sees initialization of only the lowest layer of deep models with pretrained word vectors. In this paper, they use a deep LSTM encoder from an attentional sequence-to-sequence model trained for machine translation (MT) to contextualize word vectors. They show that adding these context vectors (CoVe) improves performance over using only unsupervised word and character vectors on a wide variety of common NLP tasks: sentiment analysis (SST, IMDb), question classification (TREC), entailment (SNLI), and question answering (SQuAD). For fine-grained sentiment analysis and entailment, CoVe improves performance of our baseline models to the state of the art.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="http://papers.nips.cc/paper/7209-learned-in-translation-contextualized-word-vectors">The paper: Learned in Translation: Contextualized Word Vectors (McCann et al. NIPS 2017)</a>
</div>

# Reference 

- Paper 
  - [arXiv Version: Learned in Translation: Contextualized Word Vectors (McCann et al. arXiv 2017)](https://arxiv.org/abs/1708.00107)
  - [NIPS Version: Learned in Translation: Contextualized Word Vectors (McCann et al. NIPS 2017)](http://papers.nips.cc/paper/7209-learned-in-translation-contextualized-word-vectors)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    
- For your information
  - [NAACL 2019 Highlight on Ruder.io](http://ruder.io/naacl2019/)
  
  - Slide 
    - [Transfer Learning in Natural Language Processing tutorial on NAACL-HLT 2019](https://docs.google.com/presentation/d/1fIhGikFPnb7G5kr58OvYC3GN4io7MznnM0aAgadvJfc/edit#slide=id.g5888218f39_177_4)
































